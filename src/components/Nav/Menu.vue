<template>
  <nav class="nav">
    <div class="nav-item">
      <a class="nav-link" href="#trainings" @click.prevent="$scroll.onShowView">Виды занятий</a>
    </div>
    <div class="nav-item">
      <a class="nav-link" href="#order" @click.prevent="$scroll.onShowView">Расписание</a>
    </div>
    <div class="nav-item">
      <a class="nav-link" href="#faq" @click.prevent="$scroll.onShowView">Вопросы-ответы</a>
    </div>
    <div class="nav-item">
      <a class="nav-link" href="#partners" @click.prevent="$scroll.onShowView">Партнеры</a>
    </div>
  </nav>
</template>

<script setup>

</script>

<style scoped lang="scss">
  .nav-link {
    font-size: 18px;
    line-height: 1;
    font-weight: 400;
    letter-spacing: var(--lett-sp-sm);
    color: var(--color-text-dark);

    &:hover {
      color: var(--color-green-700);
    }
  }

  .nav {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    column-gap: 50px;
  }
</style>
