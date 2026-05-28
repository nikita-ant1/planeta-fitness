<template>
  <VDatePicker
    class="app-calendar"
    expanded
    borderless
    color="green"
    title-position="left"
    :locale="{ id: 'ru', firstDayOfWeek: 2, masks: { weekdays: 'WW', modelValue: 'YYYY-MM-DD' } }"
    :disabled-dates="disabledDates"
    :attributes="attributes"
    :min-date="from"
    v-model.string="date"
    @dayclick="onDayClick"
  />
</template>

<script setup>
  defineProps({
    disabledDates: {
      default: undefined,
      type: Array,
    },
    attributes: {
      default: undefined,
      type: Array,
    }
  });

  const emit = defineEmits([ 'change:event' ]);

  const date = defineModel();

  const from = new Date();

  function onDayClick(payload) {
    const event = payload?.attributes?.[0]?.customData ?? null;
    if(!event) return;
    emit('change:event', event);
  }
</script>

<style lang="scss">
  .app-calendar {
    --vc-font-family: 'TTturns', sans-serif;
    --vc-day-content-disabled-color: #C1C1C1;
    width: 100%;
    box-shadow: 0 4px 35px 0 rgba(170, 170, 170, 0.03);
    border-radius: 30px;

    @include sm {
      border-radius: 18px;
    }

    .vc-weeks {
      padding: 40px 35px 20px;

      @include sm {
        padding: 20px 12px 15px;
      }
    }

    .vc-header {
      margin-top: 50px;
      padding-left: 35px;
      padding-right: 35px;
      font-size: 24px;

      @include sm {
        margin-top: 20px;
        padding-left: 12px;
        padding-right: 12px;
      }

      .vc-title {
        font-size: 24px;
        font-weight: 700;
        line-height: 1;

        @include sm {
          font-size: 16px;
        }
      }
    }

    .vc-green {
      --vc-accent-600: var(--color-primary);
    }

    &.vc-light {
      --vc-weekday-color: #313131;
      --vc-header-title-color: #313131;
      --vc-color: #666666;
      --vc-day-content-disabled-color: #C1C1C1;
      --vc-bg: var(--color-white);
      --vc-header-arrow-color: #313131;
      --vc-header-arrow-hover-bg: #EDEDED;
      --vc-focus-ring: 0 0 0 2px var(--color-primary);

      .vc-attr {
        --vc-highlight-outline-content-color: #666666;
        --vc-highlight-solid-content-color: var(--color-text-dark);
      }
    }

    .vc-weekday, .vc-day-content {
      font-size: 24px;
      font-weight: 500;
      line-height: normal;

      @include sm {
        font-size: 16px;
      }
    }

    .vc-day-content {
      width: 59px;
      height: 59px;

      @include sm {
        width: 32px;
        height: 32px;
      }
    }

    .vc-highlight {
      width: 56px;
      height: 56px;

      @include sm {
        width: 30px;
        height: 30px;
      }
    }
  }
</style>
