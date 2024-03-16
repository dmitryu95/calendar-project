<template>
  <div class="main-form">
    <month-layout
        :year="$props.year"
        :month="$props.month"
        :lang = '$props.lang'
        @setMonth = 'setMonth'
        @setYear = 'setYear'/>
    <week-layout
        :lang="$props.lang"/>
    <div class="days-grid">
      <day-layout
          v-for="day in gridDays"
          :key="day"
          :day="day"
          :selectedDay="$props.selectedDay"
          @setNowDate="setNowDate"/>
    </div>
  </div>
</template>

<script>
import MonthLayout from './MonthLayout.vue'
import WeekLayout from "@/components/WeekLayout.vue";
import DayLayout from "@/components/DayLayout.vue";

export default {
  name: 'CalendarLayout',
  components: {
    DayLayout,
    WeekLayout,
    MonthLayout
  },
  props: {
    year: {
      required: true,
      type: Number
    },
    month: {
      required: true,
      type: Number
    },
    lang: {
      required: true,
      type: String
    },
    selectedDay: {
      required: true,
      type: Number
    }
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
    setMonth(month) {
      this.$emit('setMonth', month)
    },
    setYear(year) {
      this.$emit('setYear', year)
    },
    setNowDate(day) {
      this.$emit('setNowDate', day, this.month, this.year)
    }
  },
  watch: {
    month () {
        this.setGridDays()
    }
  },
  computed: {
    getCountDay() {
      return new Date(this.year, this.month, 0).getDate();
    },
    getStartWeekDay() {
      return new Date(this.year, this.month-1, 1).getDay();
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
