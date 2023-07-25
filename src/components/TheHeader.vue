<script setup>

import { ref, onMounted } from "vue";

const philosophicalQuotes = ref([
  "Выбор - ключ к смыслу нашей сущности.",
  "В выборе лежит сила обрести свою истину.",
  "Мудрость заключается в искусстве правильного выбора.",
  "Выбор - капля, формирующая океан нашей судьбы.",
  "Наши решения определяют наши пути и судьбу.",
  "Смысл жизни раскрывается через выбор сердца.",
  "Из каждого выбора рождается новое возможное будущее.",
  "Свобода - это право выбирать и ответственность за выборы.",
  "Выборы - путь к самопознанию и созиданию судьбы.",
  "Жизнь - картина, раскрашенная нашими решениями.",
  "Отважные рисуют судьбу, сделав выбор смело."
]);

let currentQuoteIndex = ref(0);

const changeQuote = () => {
  currentQuoteIndex.value = getRandomIndex();
};

const getRandomIndex = () => {
  let newIndex = Math.floor(Math.random() * philosophicalQuotes.value.length);
  
  while (newIndex === currentQuoteIndex.value) {
    newIndex = Math.floor(Math.random() * philosophicalQuotes.value.length);
  }
  return newIndex;
};

onMounted(() => {
  currentQuoteIndex.value = getRandomIndex();
  setInterval(changeQuote, 6000);
});

</script>

<template>
  <header class="header">
    <div class="header__container container">
      <h1 class="header__title">
        {{ philosophicalQuotes[currentQuoteIndex] }}
      </h1>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  padding-block: 42px;
  
  // .header__container
  &__container {
  }
  
  // .header__title
  &__title {
    text-align: center;
  }
}
</style>
