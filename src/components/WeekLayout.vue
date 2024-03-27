<template>
  <ul class="week-form__list">
    <li class="week-form__item"
      v-if="lang === 'en'"
      v-for="weekDay in daysEn"
      :key="days">
      {{ weekDay }}
    </li>
    <li class="week-form__item"
        v-else
        v-for="weekDay in daysRu"
        :key="days">
      {{ weekDay }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'WeekLayout',
  data() {
    return {
      daysEn: [
        'Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'
      ],
      daysRu: [
        'ВС', 'ПН', 'ВТ', 'СР', 'ЧТ', 'ПТ', 'СБ'
      ]
    }
  },
  props: {
    lang: "en" || "ru"
  },
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
