<template>
  <section id="partners">
    <div class="wrapper">
      <h2 class="h2 text-center title">Партнеры</h2>
      <div class="items">
        <div class="row1">
          <div class="item">
            <img class="item-img" width="100" height="100" src="@/assets/images/partners/fitness-team.svg" loading="lazy" alt="FITNESS TEAM">
          </div>
          <div class="item">
            <img class="item-img" width="119" height="124" src="@/assets/images/partners/barbara.png" loading="lazy" alt="Barbara Fitness">
          </div>
          <div class="item">
            <img class="item-img" width="175" height="82" src="@/assets/images/partners/mendeleef.svg" loading="lazy" alt="Mendeleef Fitness">
          </div>
        </div>
        <div class="row2">
          <div class="item">
            <img class="item-img" width="216" height="105" src="@/assets/images/partners/zorge.svg" loading="lazy" alt="Zorge Fitness">
          </div>
          <div class="item">
            <img class="item-img" width="155" height="92" src="@/assets/images/partners/korolef.svg" loading="lazy" alt="Korolef Fitness">
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>

</script>

<style scoped lang="scss">
  .title {
    margin-bottom: 45px;
  }

  .items {
    display: flex;
    justify-content: center;
    column-gap: 120px;

    @include lg {
      flex-wrap: wrap;
      row-gap: 35px;
    }

    @include sm {
      column-gap: 48px;
    }
  }

  .row1, .row2 {
    display: flex;
    column-gap: 120px;

    @include sm {
      column-gap: 48px;
    }
  }
</style>
