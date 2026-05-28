<template>
  <section id="trainings">
    <div class="wrapper">
      <h2 class="h2 text-center title">Выбери свою&nbsp;идеальную тренировку</h2>
      <div class="items">
        <TrainingsList class="item-list" :items="categories" @change:category="$emit('change:category', $event)" />
        <div class="item">
          <img
            class="photo"
            width="430"
            height="602"
            src="@/assets/images/woman1.jpg"
            alt="Девушка занимающаяся стрейчингом"
            loading="lazy"
          />
        </div>
        <div class="item">
          <img
            class="photo"
            width="430"
            height="602"
            src="@/assets/images/woman2.jpg"
            alt="Девушка занимающаяся бегом"
            loading="lazy"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
  import TrainingsList from '@/components/Trainings/List.vue';

  defineProps({
    categories: {
      required: true,
      type: Array,
    }
  });

  defineEmits([ 'change:category' ]);
</script>

<style scoped lang="scss">
  .title {
    margin-bottom: 45px;

    @include sm {
      margin-bottom: 30px;
    }
  }

  .items {
    display: flex;
    flex-wrap: wrap;
    align-items: flex-start;
    --col: 33.3%;
    --gap: 25px;
    margin-left: calc(var(--gap) * -1);
    margin-top: calc(var(--gap) * -1);

    @include lg {
      --col: 50%;
    }

    @include md {
      --gap: 15px;
    }

    @include sm {
      --col: 100%;
      --gap: 30px;
    }
  }

  .item, .item-list {
    width: calc(var(--col) - var(--gap));
    margin-left: var(--gap);
    margin-top: var(--gap);
  }

  .item-list {
    @include md {
      order: 1;
    }

    @include sm {
      order: -1;
    }
  }

  .photo {
    width: 100%;
    border-radius: 50px;

    @include md {
      border-radius: 40px;
    }
  }
</style>
