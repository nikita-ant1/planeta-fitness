<template>
  <main>
    <Header />
    <SectionMain class="section-main" />
    <PeriodTape class="section-tape" />
    <template v-if="data?.results">
      <SectionTrainings
        class="section-trainings"
        :categories="data.results"
        @change:category="changeCategory($event, $order.show)"
      />
      <SectionOrder
        class="section-order"
        v-model:activeCategory="activeCategory"
        :categories="data.results"
        :loading="loading"
        @finish="send"
      />
    </template>
    <SectionFaq class="section-faq" />
    <SectionPartners class="section-partners" />
    <Footer  />
    <AuthModal v-model:showed="auth.showedModal.value" @auth:completed="auth.onComplete" />
  </main>
</template>

<script setup>
  import Header from './Sections/Header.vue';
  import Footer from './Sections/Footer.vue';
  import SectionMain from './Sections/Main.vue';
  import PeriodTape from './Sections/PeriodTape.vue';
  import SectionTrainings from './Sections/Trainings.vue';
  import SectionFaq from './Sections/Faq.vue';
  import SectionPartners from './Sections/Partners.vue';
  import SectionOrder from './Sections/Order.vue';
  import AuthModal from '@/components/Auth/Modal.vue';
  import { init as initAuth } from '@/composables/useAuth';
  import useRequest from '@/composables/useRequest';
  import * as CategoriesRepo from '@/http/events';
  import { ref } from 'vue';

  const auth = initAuth();

  const { data, loading, send } = await useRequest(CategoriesRepo.all, {
    errorMessage: 'Не удалось загрузить данные!'
  });

  const activeCategory = ref(null);

  function changeCategory(category, show) {
    activeCategory.value = category;
    show();
  }
</script>

<style scoped lang="scss">
  .section-main {
    margin-bottom: 75px;

    @include md {
      margin-bottom: 50px;
    }
  }

  .section-tape {
    margin-bottom: 75px;

    @include md {
      margin-bottom: 35px;
    }
  }

  .section-trainings {
    padding: 75px 0;

    @include md {
      padding: 35px 0;
    }
  }

  .section-faq {
    padding: 75px 0;

    @include md {
      padding: 35px 0;
    }
  }

  .section-partners {
    padding: 75px 0 100px;

    @include md {
      padding: 35px 0 50px;
    }
  }

  .section-order {
    padding: 75px 0;

    @include md {
      padding: 35px 0;
    }
  }
</style>
