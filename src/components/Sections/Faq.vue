<template>
  <section id="faq">
    <div class="wrapper">
      <h2 class="h2 text-center title">Если остались вопросы</h2>
      <FaqList :items="items" />
    </div>
  </section>
</template>

<script setup>
  import FaqList from '@/components/Faq/List.vue';

  const items = [
    {
      title: 'Как попасть на&nbsp;площадку?',
      body: `
        <p>
          С улицы: со стороны улицы Энтузиастов заехать на&nbsp;крышную парковку, проехать прямо до&nbsp;входа&nbsp;№4, далее повернуть направо к&nbsp;фотозоне «ЯРКАЯ&nbsp;СТОРОНА&nbsp;ПЛАНЕТЫ».
        </p>
        <a class="app-link" href="https://ufa.planeta-mall.ru/promo/fitness/img/scheme_1.jpg" target="_blank">Смотреть карту</a>
        <br/>
        <br/>
        <p>
          Из ТРЦ: дойти до магазина «М.Видео» на&nbsp;0&nbsp;уровне, подняться на&nbsp;эскалаторе к&nbsp;выходу&nbsp;№4, пройти к&nbsp;фотозоне «ЯРКАЯ&nbsp;СТОРОНА&nbsp;ПЛАНЕТЫ».
        </p>
        <a class="app-link" href="https://ufa.planeta-mall.ru/promo/fitness/img/scheme_2.jpg" target="_blank">Смотреть карту</a>
      `,
    },
    {
      title: 'Что нужно взять с собой на занятие?',
      body: 'Рекомендуем взять с&nbsp;собой воду и&nbsp;средство от&nbsp;солнца. Мы&nbsp;также готовы предоставить свои&nbsp;коврики, но&nbsp;вы&nbsp;всегда можете захватить свой и&nbsp;сообщить нам&nbsp;об&nbsp;этом.',
    },
    {
      title: 'Кто преподаватели?',
      body: 'Молодые, энергичные, красивые и&nbsp;спортивные тренеры компании F&#8209;team.',
    },
    {
      title: 'Занятия подходят для&nbsp;новичков?',
      body: 'Наш комплекс упражнений подходит для&nbsp;начинающих и&nbsp;подготовленных участников.',
    },
    {
      title: 'Нужно ли платить за&nbsp;вход?',
      body: 'Вход бесплатный. Вам&nbsp;необходимо зарегистрироваться в&nbsp;<a class="app-link" href="https://id.mall.tech/4/auth" target="_blank">Личном&nbsp;кабинете</a>. Рекомендуем приходить на&nbsp;тренировку за&nbsp;10-15&nbsp;минут до&nbsp;её&nbsp;начала для&nbsp;комфортной подготовки к&nbsp;тренировке.',
    },
    {
      title: 'Нужно ли подтверждать запись?',
      body: 'Не нужно.',
    },
  ];
</script>

<style scoped lang="scss">
  .title {
    margin-bottom: 35px;
  }
</style>
