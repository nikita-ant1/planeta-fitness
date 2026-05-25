<template>
  <div class="list-block">
    <div class="list-wrap">
      <ul class="list scroll-x">
        <li
          class="item"
          v-for="item in items"
          :key="item.id"
        >
          <button class="item-btn" type="button" @click="$emit('change:category', item)">
            {{ item.title }}
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
  defineProps({
    items: {
      required: true,
      type: Array,
    }
  });

  defineEmits([ 'change:category' ]);
</script>

<style scoped lang="scss">
  .list-block {
    border-radius: 50px;
    background: #313634;
    position: relative;

    @include md {
      border-radius: 40px;
    }

    &::before {
      content: '';
      display: block;
      width: 100%;
      padding-top: 140%;

      @include sm {
        padding-top: 0;
      }
    }
  }

  .list-wrap {
    padding: 40px;
    padding-right: 24px;
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    z-index: 1;

    @include sm {
      position: static;
    }

    @include md {
      padding: 30px;
      padding-right: 15px;
    }
  }

  .list {
    padding-right: 16px;
    width: 100%;
    height: 100%;
    overflow-x: hidden;

    @include sm {
      max-height: 450px;
    }
  }

  .item {
    & + & {
      margin-top: 12px;

      @include md {
        margin-top: 5px;
      }

      @include sm {
        margin-top: 0px;
      }
    }
  }

  .item-btn {
    display: block;
    width: 100%;
    padding: 10px 0;
    color: #DDDDDD;
    text-align: left;
    font-size: 20px;
    line-height: 1.2;
    font-weight: 400;
    letter-spacing: var(--lett-sp-sm);
    transition: transform 150ms;

    @include md {
      font-size: 18px;
    }

    &:hover {
      color: var(--color-primary);
      transform: translateX(10px);
    }
  }
</style>
