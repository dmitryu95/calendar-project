<template>
  <div class="main-form">
    <month-and-year-layout
        :date = 'date'
        :lang = 'lang'
        @setDate="setDate"/>
    <week-layout
        :lang="lang"/>
    <div class="days-grid">
      <day-layout
          v-for="day in gridDays"
          :key = "day"
          :day = 'day'
          @click="setDateToday(day)"/>
    </div>
  </div>
</template>

<script>
import WeekLayout from "@/components/WeekLayout.vue";
import DayLayout from "@/components/DayLayout.vue";
import MonthAndYearLayout from "@/components/MonthAndYearLayout.vue";

export default {
  name: 'CalendarLayout',
  components: {
    DayLayout,
    WeekLayout,
    MonthAndYearLayout
  },
  props: {
    date: {
      year: Number,
      month: Number,
      day: Number
    },
    lang: {
      required: true,
      type: String
    },
  },
  data() {
    return {
      gridDays: []
    };
  },
  mounted() {
    this.setGridDays()
  },
  methods: {
    setGridDays() {
      this.gridDays = [];

      for (let j = 1; j <= this.getStartWeekDay; j++ ) {
        this.gridDays.push(0);
      }
      for (let i = 1; i <= this.getCountDay; i++) {
        this.gridDays.push(i);
      }
    },
    setDate(date) {
      this.$emit('setDate', date )
    },
    setDateToday(day) {
      this.$emit('setDateToday', { day: day, month: this.date.month, year: this.date.year })
    },
  },
  watch: {
    date() {
      this.setGridDays();
    }
  },
  computed: {
    getCountDay() {
      return new Date(this.date.year, this.date.month, 0).getDate();
    },
    getStartWeekDay() {
      return new Date(this.date.year, this.date.month-1, 1).getDay();
    },
  }
};
</script>

<style>
.main-form {
  position: relative;
  width: 70vw;
  border: 2px solid #2c3e50;
  display: flex;
  flex-direction: column;
}

.days-grid {
  display: flex;
  flex-wrap: wrap;
}
</style>
