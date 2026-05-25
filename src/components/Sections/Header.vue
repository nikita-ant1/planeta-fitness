<template>
  <header class="header">
    <div class="wrapper">
      <div class="wrap">
        <a class="logo-wrap" href="https://ufa.planeta-mall.ru/" target="_blank">
          <img class="logo" src="@/assets/images/logo.svg" width="184" height="59" alt="Логотип Планета">
        </a>
        <NavMenu v-if="grid.lg" />
        <button v-else class="btn-burger" @click="showed = true">
          <BaseIcon name="burger" fit />
        </button>
      </div>
    </div>
    <NavScreen v-if="!grid.lg" :showed="showed" @close="showed = false" />
  </header>
</template>

<script setup>
  import NavMenu from '@/components/Nav/Menu.vue';
  import NavScreen from '@/components/Nav/Screen.vue';
  import useAppGrid from '@/composables/useAppGrid';
  import { ref } from 'vue';

  const grid = useAppGrid();

  const showed = ref(false);
</script>

<style scoped lang="scss">
  .header {
    padding: 30px 0;

    @include md {
      padding: 24px 0;
    }
  }

  .wrap {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: space-between;
    column-gap: 50px;
  }

  .logo-wrap {
    width: 184px;

    &:hover {
      opacity: 0.7;
    }

    @include md {
      width: 160px;
    }

    @include sm {
      width: 143px;
    }
  }

  .btn-burger {
    cursor: pointer;
    width: 32px;
    height: 32px;
    flex-shrink: 0;
    color: var(--color-text-dark);
  }
</style>
