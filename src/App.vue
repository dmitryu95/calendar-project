<template>
  <h1>Calendar</h1>
  <h2>{{selectedDate}}</h2>
  <button class="btn-change-language"
          @click="setLanguage">
    {{ btnName }}
  </button>
  <calendar-layout
    :month='month'
    :year='year'
    :lang="lang"
    :selectedDay="selectedDay"
    @setMonth="setMonth"
    @setYear="setYear"
    @setNowDate="setNowDate"/>
</template>

<script>
import CalendarLayout from './components/CalendarLayout.vue'

export default {
  name: 'App',
  components: {
    CalendarLayout
  },

  data() {
    return {
      year: new Date().getFullYear(),
      month: new Date().getMonth()+1,
      selectedDay: new Date().getUTCDate(),
      selectedDate: `${new Date().getUTCDate()} -
        ${new Date().getMonth()+1} -
        ${new Date().getFullYear()}`,
      lang: 'en',
      btnName: 'Change language',
    }
  },
  methods: {
    setMonth(month) {
      this.month = month
    },
    setYear(year) {
      this.year = year
    },
    setLanguage() {
      if(this.lang === 'en') {
        this.lang = 'ru'
        this.btnName = 'Сменить язык'
      } else {
        this.lang = 'en'
        this.btnName = 'Change language'
      }
    },
    setNowDate(day, month, year) {
      this.selectedDay = day
      this.month = month
      this.year = year

      this.selectedDate = `${day} - ${month} - ${year}`

      return this.selectedDate
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;

  .btn-change-language {
    display: flex;
    margin: 10px;
    height: 30px;
    align-items: center;
    font-size: medium;
    border-radius: 7px;
  }
}


</style>
