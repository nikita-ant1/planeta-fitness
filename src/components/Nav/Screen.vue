<template>
  <Teleport to="body">
    <Transition name="nav-anim">
      <div class="nav-mobile" v-if="showed">
        <div class="wrapper">
          <div class="body">
            <div class="head">
              <a class="logo" href="https://ufa.planeta-mall.ru/" target="_blank">
                <img class="logo-img" src="@/assets/images/logo-white.svg" width="143" height="46" alt="Логотип Планета">
              </a>
              <button class="btn-close" @click="$emit('close')">
                <BaseIcon name="close" fit />
              </button>
            </div>
            <div class="nav">
              <div class="nav-wrap">
                <a class="nav-link" href="#trainings" @click.prevent="$scroll.onShowView($event); emit('close')">
                  Виды занятий
                </a>
              </div>
              <div class="nav-wrap">
                <a class="nav-link" href="#order" @click.prevent="$scroll.onShowView($event); emit('close')">
                  Расписание
                </a>
              </div>
              <div class="nav-wrap">
                <a class="nav-link" href="#faq" @click.prevent="$scroll.onShowView($event); emit('close')">
                  Вопросы-ответы
                </a>
              </div>
              <div class="nav-wrap">
                <a class="nav-link" href="#partners" @click.prevent="$scroll.onShowView($event); emit('close')">
                  Партнеры
                </a>
              </div>
            </div>
            <div>
              <BaseButton class="order-btn" @click="$order.show(); emit('close')">
                Записаться
              </BaseButton>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
  defineProps({
    showed: {
      required: true,
      type: Boolean,
    },
  });

  const emit = defineEmits([ 'close' ]);
</script>

<style scoped lang="scss">
  .nav-mobile {
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 9000;
    background-color: #313634;
    overflow-x: hidden;
    padding-bottom: 32px;
  }

  .body {
    padding-top: 24px;
  }

  .head {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 30px;
  }

  .nav-anim {
    &-enter-from {
      opacity: 0;
    }

    &-enter-active {
      transition: opacity 300ms;
    }

    &-leave-active {
      transition: opacity 300ms;
      opacity: 0;
    }
  }

  .nav {
    margin-bottom: 50px;
  }

  .nav-wrap {
    padding: 12px 0;
  }

  .nav-link {
    font-weight: 400;
    font-size: 18px;
    line-height: 1;
    color: var(--color-white);
    letter-spacing: var(--lett-sp-sm);
  }

  .btn-close {
    cursor: pointer;
    width: 32px;
    height: 32px;
    padding: 4px;
    color: var(--color-white);
  }

  .logo {
    width: 160px;

    @include sm {
      width: 143px;
    }

    &-img {
      width: 100%;
    }
  }

  .order-btn {
    width: 100%;
    max-width: 365px;

    @include sm {
      max-width: 100%;
    }
  }
</style>
