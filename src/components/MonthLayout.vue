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
      <span>{{year}}</span>
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
  name: 'MonthLayout',
  props: {
    year: {
      required: true,
      type: Number
    },
    month: {
      required: true,
      type: Number
    },
    lang: String
  },
  methods: {
    setMonth(num, event) {
      let selectedMonth = this.month + num;

      if (selectedMonth < 0) {
        selectedMonth = 11;
      } else if (selectedMonth > 11) {
        selectedMonth = 0;
      }

      this.$emit('setMonth', selectedMonth);
      this.setYear(event);
    },
    setYear(event) {
      let selectedYear = this.year

      if (event === 'next' && this.month === 0) {
        selectedYear += 1
      } else if (event === 'prev' && this.month === 1) {
        selectedYear -= 1
      }

      this.$emit('setYear', selectedYear);
    },
  },
  computed: {
    setMonthName() {
      let nameMonth = new Date(this.year, this.month-1)

      if(this.lang === 'ru') {
        return monthNames[this.month]
      }

      return nameMonth.toLocaleString('default', { month: 'long' })
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
