<template>
  <div class="day-form__item"
       :class="day === 0 ? 'empty' : 'some-value'">
    {{ day }}
  </div>
</template>

<script>
export default {
  name: 'DayLayout',
  props: {
    day: Number
  },
}
</script>


<style>
.day-form__item {
  display: flex;
  height: 10vh;
  width: 10vw;
  text-align: center;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  box-sizing: border-box;
}

.empty {
  opacity: 0;
}

.some-value {
  opacity: 1;
}
</style>

