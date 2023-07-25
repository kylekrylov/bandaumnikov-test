<script setup>

import Button from "@/components/Atom/Button.vue";

import { defineProps, ref } from "vue";
import IconImage from "@/components/Atom/Icons/Image.vue";

const props = defineProps({
  item: {
    type:Object,
    default: ()=> {}
  }
})

const item = ref(props.item)

// Функция для поделиться выбранным кафе
const shareCafe = (id) => {
  const cafeUrl = `https://bandaumnikov.ru/api/test/site/get-view?id=${id}`;
  // Поделиться ссылкой с друзьями
  alert(`Ссылка скопирована: ${cafeUrl}`)
};
</script>

<template>
  <li
    :key="item.id"
    class="item"
    v-if="item.address"
  >
    <div class="item__cover">
      <img
        v-if="item.photo"
        class="item__img"
        :src="item.photo"
        alt=""
      >
      <IconImage v-else class="item__not-img"/>
    </div>
    <div class="item__body">
      <div class="item__title">
        {{ item.name }}
      </div>
      <div
        class="item__location"
      >
        Адрес:
        <span class="item__address">
          {{ item.address }}
        </span>
      </div>
      <div class="item__description">
        <div
          v-if="item.price"
          class="item__price"
        >
          <span class="item__subtitle">
            Средний чек:
          </span> {{ item.price }} ₽
        </div>
        <div
          v-if="item.landmark"
          class="item__landmark"
        >
          <span class="item__subtitle">
            Как найти:
          </span> {{ item.landmark }}
        </div>
        <div
          v-if="item.cuisine"
          class="item__cuisine"
        >
          <span class="item__subtitle">
            Кухня:
          </span>{{ item.cuisine }}
        </div>
        <div
          v-if="item.business_lunch"
          class="item__business-lunch"
        >
          <span class="item__subtitle">
            Бизнес ланч:
          </span> есть
        </div>
        <div
          v-if="item.distance"
          class="item__distance"
        >
          <span class="item__subtitle">
            Расстояние:
          </span> {{ item.distance }} м.
        </div>
        <div class="item__time" v-if="item.time">
          <span class="item__subtitle">
            Сколько добираться:
          </span> {{ item.time }} минут
        </div>
      </div>
      <Button
        color-btn="fill"
        class="item__button"
        @click="shareCafe(item.id)"
      >
        Поделиться
      </Button>
    </div>
  </li>
</template>

<style scoped lang="scss">

.item {
  display: flex;
  flex-direction: column;
  padding: 12px;
  border: 2px solid var(--color-border);
  border-radius: 20px;
  transition: border .2s ease-in-out;
  
  &:hover {
    border-color: var(--vt-c-main);
  }
  
  &__cover {
    position: relative;
    
    display: flex;
    flex-shrink: 0;
    justify-content: center;
    align-items: center;
    height: 200px;
    margin-bottom: 12px;
    border: 2px var(--vt-c-main) solid;
    border-radius: 8px;
    overflow: hidden;
  }
  
  &__img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  &__not-img {
    width: 60px;
    height: 60px;
    fill: #00bd7e;
  }
  
  &__body {
    display: flex;
    flex-direction: column;
    height: 100%;
  }
  
  &__title {
    margin-bottom: 12px;
    font-size: 20px;
    font-weight: bold;
  }
  
  &__location {
    margin-bottom: 12px;
  }
  
  // .item__subtitle
  &__subtitle {
    font-weight: 300;
  }
  
  &__address {
    font-size: 14px;
  }
  
  &__description {
    color: var(--color-text-1);
    font-size: 14px;
  }
  
  &__price {
    margin-bottom: 6px;
  }
  
  &__landmark,
  &__distance,
  &__time,
  &__cuisine,
  &__business-lunch {
    margin-bottom: 4px;
  }
  
  // .item__time
  &__time {
    margin-bottom: 8px;
  }
  
  // .item__button
  &__button {
    margin-top: auto;
  }
}
</style>
