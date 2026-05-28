<template>
  <div class="main-block">
    <div class="wrapper">
      <div class="banner">
        <div class="banner__title-wrap">
          <h1 class="banner__title">Фитнес<br>на крыше</h1>
        </div>
        <div class="banner__period-wrap">
          <p class="banner__period">июнь-сент</p>
        </div>
        <div class="banner__text-wrap" v-if="grid.md">
          <p class="banner__text">
            <span class="banner__text-l1">каждый день</span>
            <span class="banner__text-l2">бесплатные занятия</span>
            <span class="banner__text-l3">вместе</span>
            <span class="banner__text-l4">с F-team</span>
          </p>
        </div>
        <picture>
          <source media="(max-width: 767.9px)" width="750" height="1080" srcset="@/assets/images/banner-sm.jpg" />
          <source media="(min-width: 768px)" width="2011" height="1131" srcset="@/assets/images/banner.jpg" />
          <img class="banner__img" src="@/assets/images/banner.jpg" width="2011" height="1131" alt="Фитнес на Крыше">
        </picture>
      </div>
      <div v-if="!grid.md" class="banner__text-sm-wrap">
        <p class="banner__text-sm">
          каждый день<br>бесплатные занятия<br>вместе с F-team<br>на крыше Планеты
        </p>
      </div>
      <div class="order-wrap">
        <BaseButton class="order" @click="$order.show">Записаться</BaseButton>
      </div>
    </div>
  </div>
</template>

<script setup>
  import useAppGrid from '@/composables/useAppGrid';

  const grid = useAppGrid();
</script>

<style scoped lang="scss">
  .order-wrap {
    width: 100%;
    text-align: center;
  }

  .order {
    width: 100%;
    max-width: 365px;
  }

  .banner {
    position: relative;
    border-radius: 50px;
    overflow: hidden;
    margin-bottom: 50px;

    @include md {
      border-radius: 40px;
      margin-bottom: 30px;
    }

    @include sm {
      margin: 0 -16px 20px;
      border-radius: 24px;
    }

    &__img {
      width: 100%;
    }

    &__text-sm-wrap {
      margin-bottom: 24px;
    }

    &__text-sm {
      padding-left: 24px;
      font-weight: 400;
      font-size: 20px;
      line-height: 1.2;
      letter-spacing: 0.03em;
    }

    &__title-wrap {
      position: absolute;
      right: 17%;
      bottom: 10.8%;

      @include sm {
        left: 12.6%;
        bottom: 7.6%;
      }
    }

    &__title {
      font-weight: 600;
      letter-spacing: 0.02em;
      line-height: 1;
      font-size: clamp(30px, 5.2vw, 103px);

      @include sm {
        font-size: clamp(32px, 11.7vw, 90px);
      }
    }

    &__period-wrap {
      position: absolute;
      left: 30%;
      bottom: 8.6%;

      @include sm {
        left: 13%;
        bottom: 26%;
      }
    }

    &__period {
      font-weight: 500;
      line-height: 1.2;
      font-size: clamp(20px, 3.7vw, 75px);

      @include sm {
        line-height: 1;
        font-weight: 600;
        font-size: clamp(18px, 8vw, 62px);
      }
    }

    &__text-wrap {
      position: absolute;
      left: 6%;
      bottom: 9.5%;
    }

    &__text {
      font-weight: 400;
      line-height: 1.1;
      letter-spacing: 0.03em;
      font-size: clamp(16px, 2.5vw, 50px);
      color: var(--color-white);

      &-l1, &-l2, &-l3, &-l4 {
        display: block;
        width: fit-content;
      }

      &-l1 {
        padding-left: 1.64em;
      }

      &-l2 {}

      &-l3 {
        padding-left: 0.58em;
      }

      &-l4 {
        padding-left: 1.86em;
      }
    }
  }
</style>
