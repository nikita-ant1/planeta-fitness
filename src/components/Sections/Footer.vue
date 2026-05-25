<template>
  <footer class="footer">
    <div class="wrapper">
      <div class="footer__wrap">
        <div class="footer__body">
          <div class="footer__address">
            <p class="footer__name">ТРЦ «Планета»</p>
            <p>г. Уфа, ул. Энтузиастов, 20</p>
          </div>
          <div class="soc-items">
            <a class="soc-item soc-item--tg" href="https://t.me/trc_planeta_ufa" target="_blank"></a>
            <a class="soc-item soc-item--max" href="https://max.ru/trc_planeta_ufa" target="_blank"></a>
          </div>
        </div>
        <a class="logo" href="https://ufa.planeta-mall.ru/" target="_blank">
          <img class="logo__img" width="184" height="59" src="@/assets/images/logo.svg" alt="Логотип планета">
        </a>
      </div>
    </div>
  </footer>
</template>

<script setup></script>

<style scoped lang="scss">
  .footer {
    padding: 48px 0;

    @include sm {
      padding: 35px 0;
    }

    &__wrap {
      display: flex;
      flex-wrap: wrap;
      align-items: flex-start;
      justify-content: space-between;
      row-gap: 24px;
    }

    &__address {
      font-weight: 400;
      font-size: 20px;
      line-height: 1;
      letter-spacing: var(--lett-sp-sm);
      margin-bottom: 30px;

      @include sm {
        font-size: 16px;
        margin-bottom: 20px;
      }
    }

    &__body {
      @include sm {
        width: 100%;
        order: 1;
      }
    }

    &__name {
      margin-bottom: 10px;
    }
  }

  .logo {
    width: 184px;

    @include md {
      width: 160px;
    }

    @include sm {
      width: 143px;
    }

    &:hover {
      opacity: 0.7;
    }

    &__img {
      width: 100%;
    }
  }

  .soc-items {
    display: flex;
    align-items: flex-start;
    column-gap: 16px;
  }

  .soc-item {
    width: 32px;
    height: 32px;
    flex-shrink: 0;
    background-size: 100%;

    &:hover {
      opacity: 0.8;
    }

    &--max {
      background-image: url('@/assets/images/soc/max.svg');
    }

    &--vk {
      background-image: url('@/assets/images/soc/vk.svg');
    }

    &--ok {
      background-image: url('@/assets/images/soc/ok.svg');
    }

    &--rt {
      background-image: url('@/assets/images/soc/rt.svg');
    }

    &--tg {
      background-image: url('@/assets/images/soc/tg.svg');
    }

    &--you {
      background-image: url('@/assets/images/soc/you.svg');
    }
  }
</style>
