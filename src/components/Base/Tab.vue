<template>
  <button class="tab" :class="[ active ? 'tab--active' : 'tab--default' ]">
    <span class="circle"></span>
    <span>{{ text }}</span>
  </button>
</template>

<script setup>
  defineProps({
    text: {
      required: true,
      type: String,
    },
    active: {
      default: false,
      type: Boolean,
    },
    color: {
      default: '#000',
      type: String,
    }
  })
</script>

<style scoped lang="scss">
  .tab {
    border-radius: 30px;
    padding: 16px 20px;
    border: 1px solid var(--border-color);
    color: var(--text-color);
    background: var(--bg-color);
    font-weight: 400;
    font-size: 18px;
    line-height: 1;
    letter-spacing: var(--lett-sp-sm);
    display: flex;
    align-items: center;
    gap: 10px;

    &:hover {
      opacity: 0.7;
    }

    &--default {
      --text-color: #212123;
      --border-color: #B5B5B5;
      --bg-color: var(--color-white);
      --circle-color: v-bind(color);
    }

    &--active {
      --text-color: var(--color-white);
      --border-color: v-bind(color);
      --bg-color: v-bind(color);
      --circle-color: var(--color-white);

      &:hover {
        opacity: 1;
      }
    }
  }

  .circle {
    width: 10px;
    height: 10px;
    flex-shrink: 0;
    border-radius: 50%;
    background: var(--circle-color);
  }
</style>
