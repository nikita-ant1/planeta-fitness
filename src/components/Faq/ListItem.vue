<template>
  <article class="item">
    <div class="head" @click="showed = !showed">
      <h3 class="title" v-html="title"></h3>
      <button class="btn" :class="{ 'btn--active': showed }" type="button">
        <BaseIcon
          class="w-full h-full"
          name="plus"
        />
      </button>
    </div>
    <SlideUpDown :active="showed" :duration="300">
      <div class="body" v-html="body"></div>
    </SlideUpDown>
  </article>
</template>

<script setup>
  import { ref } from 'vue';
  import SlideUpDown from 'vue-slide-up-down';

  defineProps({
    title: {
      required: true,
      type: String,
    },
    body: {
      required: true,
      type: String,
    },
  });

  const showed = ref(false);
</script>

<style scoped lang="scss">
  .item {
    padding: 30px 50px;
    border-radius: 40px;
    background: var(--color-white);
    color: var(--color-text-dark);

    @include sm {
      padding: 20px 24px;
      border-radius: 24px;
    }
  }

  .btn {
    flex-shrink: 0;
    width: 40px;
    height: 40px;
    transition: transform 150ms;

    &--active {
      transform: rotate(45deg);
    }
  }

  .head {
    display: flex;
    align-items: center;
    column-gap: 30px;
    cursor: pointer;
    user-select: none;

    &:hover {
      opacity: 0.8;
    }
  }

  .title {
    font-weight: 400;
    font-size: 18px;
    line-height: 1;
    letter-spacing: var(--lett-sp-sm);
    flex-grow: 1;

    @include sm {
      font-size: 18px;
      line-height: 1.2;
    }
  }

  .body {
    padding-top: 20px;
    font-size: 16px;
    letter-spacing: var(--lett-sp-sm);
    line-height: 1.3;
  }
</style>
