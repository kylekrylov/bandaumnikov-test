<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

import Cafeteria from "@/components/Moleculs/Cafeteria.vue";
import Button from "@/components/Atom/Button.vue";

// Список кафе
const cafes = ref([]);
let length = ref(null);

// Загрузка списка кафе при загрузке компонента
onMounted(() => {
  getCafes();
  length.value = cafes.value.length
});

function throttle(callback, timeout) {
  let timer = null;
  
  return function perform(...args) {
    if (timer) return;
    timer = setTimeout(() => {
      callback(...args);
      clearTimeout(timer);
      timer = null;
    }, timeout);
  };
}

// Функция для загрузки списка кафе
const getCafes = async () => {
  const url = 'https://bandaumnikov.ru/api/test/site/get-index'
  
  try {
    const response = await axios.get(url);
    cafes.value = response.data.data;
    length.value = cafes.value.length
    
  } catch (error) {
    console.error('Ошибка при загрузке данных:', error);
  }
};

// Функция для выбора случайного кафе
const getRandomCafe = async () => {
  const url = 'https://bandaumnikov.ru/api/test/site/get-view';
  cafes.value = [];
  
  try {
    const randomIndex = Math.floor(Math.random() * length.value);
    const response = await axios.get(`${url}?id=${randomIndex}`);
    const data = response.data.data;
    
    if (!data.address) getRandomCafe();
    
    cafes.value.push(data);
    return data;
    
  } catch (error) {
    console.error('Ошибка при загрузке данных:', error);
  }
};

</script>

<template>
  <div class="cafeterias">
    <div class="cafeterias__buttons">
      <Button
        color-btn="fill"
        @click="getRandomCafe"
      >
        Выбрать случайное кафе
      </Button>
      <Button
        color-btn="fill"
        @click="getCafes"
      >
        Показать все ближайшие
      </Button>
    </div>
    <h2
      v-if="cafes.length > 0"
      class="cafeterias__title"
    >
      {{ cafes.length <= 1 ? 'Кафешка:' : 'Список кафешек:' }}
    </h2>
    <ul class="cafeterias__list">
      <Cafeteria
        v-for="cafe in cafes"
        :key="cafe.id"
        :item="cafe"
      />
    </ul>
  </div>
</template>

<style scoped lang="scss">

.cafeterias {
  padding-block: 34px;
  display: grid;
  grid-gap: 24px;
  
  
  &__buttons {
    display: grid;
    grid-gap: 12px;
    grid-template-columns: repeat(auto-fill, minmax(272px, 1fr));
  }
  
  &__title {
    font-size: 24px;
    font-weight: 600;
  }
  
  &__list {
    display: grid;
    grid-gap: 12px;
    grid-template-columns: repeat(auto-fill, minmax(272px, 1fr));
  }
}

</style>
