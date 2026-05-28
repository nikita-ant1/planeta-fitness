<template>
  <section id="order" class="section-order">
    <div class="wrapper">
      <h2 class="h2 section-order__title">Запишись на удобное&nbsp;время</h2>
      <div class="section-order__grid">
        <div class="section-order__left">
          <Calendar v-model="orderDate" :disabledDates="disabledDates" :attributes="calendarAttrs" @change:event="activeEvent = $event" />
          <Transition
            v-if="!grid.lg"
            enter-active-class="animate__animated animate__zoomIn anim-fast"
            leave-active-class="animate__animated animate__zoomOut anim-fast"
          >
            <ActiveEvent
              class="section-order__event"
              v-if="activeEvent && orderDate"
              :event="activeEvent"
            >
              <template #actions>
                <BaseButton
                  class="section-order__btn"
                  :disabled="!canOrder"
                  @click="createOrderAction"
                >
                  Записаться
                </BaseButton>
              </template>
            </ActiveEvent>
          </Transition>
        </div>
        <div class="section-order__right">
          <div class="working-time">
            <BaseBadge class="working-time__badge">Будни в 20:30</BaseBadge>
            <BaseBadge class="working-time__badge">Выходные в 11:00</BaseBadge>
          </div>
          <Categories :items="categories" v-model:activeItem="activeCategory" />
          <Transition
            v-if="grid.lg"
            enter-active-class="animate__animated animate__zoomIn anim-fast"
            leave-active-class="animate__animated animate__zoomOut anim-fast"
          >
            <ActiveEvent
              class="section-order__event"
              v-if="activeEvent && orderDate"
              :event="activeEvent"
            >
              <template #actions>
                <BaseButton
                  class="section-order__btn"
                  :disabled="!canOrder"
                  @click="createOrderAction"
                >
                  Записаться
                </BaseButton>
              </template>
            </ActiveEvent>
          </Transition>
        </div>
      </div>
    </div>
    <SuccessModal
      v-model:showed="successModal"
      :event="activeEvent"
      @finish="finish"
    />
    <BaseInnerLoading :showed="loading" />
  </section>
</template>

<script setup>
  import Calendar from '@/components/Order/Calendar.vue';
  import Categories from '@/components/Order/Categories.vue';
  import ActiveEvent from '@/components/Order/ActiveEvent.vue';
  import useAuth from '@/composables/useAuth';
  import * as OrderRepo from '@/http/order';
  import { computed, ref, watch } from 'vue';
  import { dateToIso } from '@/helpers/dates';
  import SuccessModal from '../Order/SuccessModal.vue';
  import { useNotification } from '@kyvg/vue3-notification';
  import useForm from '@/composables/useForm';
  import useAppGrid from '@/composables/useAppGrid';

  const props = defineProps({
    categories: {
      required: true,
      type: Array,
    },
    loading: {
      default: false,
      type: Boolean,
    },
  });

  const emit = defineEmits([ 'finish' ]);

  const grid = useAppGrid();

  const orderDate = ref('');
  const activeEvent = ref(null);
  const activeCategory = defineModel('activeCategory', { required: true, type: [Object, null] });

  watch(activeCategory, () => {
    orderDate.value = '';
    activeEvent.value = null;
  });

  watch(orderDate, (date) => {
    if(date) {
      scrollToCalendar();
    }
  });

  const disabledDates = computed(() => {
    function isDisabled(event, _opts) {
      const dt1 = event.start_date.split(' ')[0];
      const dt2 = dateToIso(_opts.date);
      return dt1 !== dt2;
    }

    const start = new Date();
    start.setDate(start.getDate() - 1);

    function makeEverydayPattern(onFn) {
      return [
        {
          start,
          repeat: {
            every: 'day',
            on: onFn,
          }
        }
      ]
    }

    if(!activeCategory.value) {
      return makeEverydayPattern((_opts) => {
        return props.categories
          .every(item => {
            return item.events.every(event => isDisabled(event, _opts));
          });
      });
    }

    return makeEverydayPattern((_opts) => {
      return activeCategory.value.events
        .every(event => isDisabled(event, _opts));
    });
  });

  const calendarAttrs = computed(() => {
    function makeHighlight(color) {
      return {
        fillMode: 'outline',
        style: {
          borderColor: color,
        },
      };
    }

    if(!activeCategory.value) {
      return props.categories.reduce((acc, item) => {
        item.events.forEach(event => {
          acc.push({
            dates: new Date(event.start_date),
            highlight: orderDate.value === '' ? makeHighlight(item.color) : undefined,
            customData: { ...event, name: item.title },
          });
        });

        return acc;
      }, []);
    }

    return activeCategory.value.events.map(event => {
      return {
        dates: new Date(event.start_date),
        highlight: makeHighlight(activeCategory.value.color),
        customData: { ...event, name: activeCategory.value.title },
      }
    });
  });

  const { notify } = useNotification();
  const successModal = ref(false);
  const auth = useAuth();

  function orderFn(_form, { event: user }) {
    return OrderRepo.create(user.api_token, {
      event_id: activeEvent.value?.id,
      user_id: user.id,
    });
  }

  function successFn(res) {
    if(!res.data.success) {
      notify({
        type: 'error',
        text: res.data.error,
      });
    } else {
      successModal.value = true;
    }
  }

  const { pending: orderPending, onSubmit: createOrder } = useForm(orderFn, {}, successFn);

  const createOrderAction = auth.addAction(createOrder);

  const canOrder = computed(() => {
    return activeEvent.value && !orderPending.value;
  });

  function finish() {
    orderDate.value = '';
    activeCategory.value = null;
    activeEvent.value = null;
    emit('finish');
  }

  function scrollToCalendar() {
    const calendar = document.querySelector('.app-calendar');
    if(!calendar) return;
    const y = window.scrollY + calendar.getBoundingClientRect().top - 10;
    window.scrollTo({ top: y, behavior: 'smooth' });
  }
</script>

<style scoped lang="scss">
  .section-order {
    position: relative;

    &__title {
      text-align: center;
      margin-bottom: 45px;

      @include sm {
        margin-bottom: 24px;
      }
    }

    &__grid {
      --gap-x: 40px;
      --col1: 45%;
      --col2: 55%;
      display: flex;
      flex-wrap: wrap;
      column-gap: var(--gap-x);

      @include lg {
        --col1: 55%;
        --col2: 45%;
      }

      @include md {
        --col1: 100%;
        --col2: 100%;
        --gap-x: 0px;
        row-gap: 24px;
      }
    }

    &__left {
      width: calc(var(--col1) - (var(--gap-x) / 2));
    }

    &__right {
      width: calc(var(--col2) - (var(--gap-x) / 2));

      @include md {
        order: -1;
      }
    }

    &__event {
      margin-top: 40px;

      @include sm {
        margin-top: 24px;
      }
    }

    &__btn {
      width: 100%;
      max-width: 250px;

      @include sm {
        max-width: 100%;
      }
    }
  }

  .working-time {
    display: flex;
    gap: 16px;
    margin-bottom: 40px;

    @include md {
      margin-bottom: 24px;
    }

    @include sm {
      gap: 8px;
    }

    &__badge {
      width: 100%;
      max-width: 250px;

      @include md {
        max-width: 100%;
      }

      &.badge {
        @include lg {
          font-size: 16px;
          padding: 14px 16px;
        }

        @include md {
          padding: 16px;
        }

        @include sm {
          font-size: 14px;
        }
      }
    }
  }

  .anim-fast {
    --animate-duration: 300ms;
  }
</style>
