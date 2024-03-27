<template>
  <div class="month-year-form">
    <button class="scroll-date left"
      type="button"
      @click="setMonth(-1, 'prev')">
      ◀
    </button>
    <div>
      <span>{{setMonthName}}</span>
    </div>
    <div>
      <span>{{date.year}}</span>
    </div>
    <button class="scroll-date right"
      type="button"
      @click="setMonth(1, 'next')">
      ▶
    </button>
  </div>
</template>

<script>
import monthNames from '@/assets/MonthNames'
export default {
  name: 'MonthAndYearLayout',
  props: {
    date: {
      year: Number,
      month: Number,
      day: Number,
    },
    lang: String
  },
  methods: {
    setMonth(num, event) {
      let selectedMonth = this.date.month + num;

      if (selectedMonth < 0) {
        selectedMonth = 11;
      } else if (selectedMonth > 11) {
        selectedMonth = 0;
      }

      this.setYear(event, selectedMonth);
    },
    setYear(event, month) {
      let year = this.date.year

      if (event === 'next' && month === 0) {
        year += 1
      } else if (event === 'prev' && month === 1) {
        year -= 1
      }

      this.$emit('setDate',{ day: this.date.day, month, year} );
    },
  },
  computed: {
    setMonthName() {
      let nameMonth = new Date(this.date.year, this.date.month-1)

      return this.lang === 'ru' ? monthNames[this.date.month] :
          nameMonth.toLocaleString('default', { month: 'long' })
    },
  }
}
</script>

<style>
span {
  margin: 0 10px;
}
.month-year-form {
  width: 100%;
  height: 5vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.scroll-date {
  display: flex;
  position: absolute;
  border: none;
  background: none;
  font-size: 20px;
}

.left {
 left: 10px
}

.right {
  right: 10px;
}
</style>
