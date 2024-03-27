<template>
  <ul class="week-form__list">
    <li class="week-form__item"
        v-for="weekDay in days"
        :key="weekDay">
      {{ weekDay }}
    </li>
  </ul>
</template>

<script>
import {WEEK_RU, WEEK_EN } from '@/assets/MonthNames'
export default {
  name: 'WeekLayout',
  props: {
    lang: "en" || "ru"
  },
  computed: {
    days() {
      return (this.lang === 'en') ? WEEK_EN : WEEK_RU
    }
  }
}
</script>

<style>
.week-form__list {
  list-style-type: none;
  display: flex;
  justify-content: space-around;
  margin: 10px 0;
  padding: 0;
}

.week-form__item {
  width: 10vh;
}
</style>
