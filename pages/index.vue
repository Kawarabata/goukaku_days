<template>
  <div class="days-calculator">
    <h2>合格までの日数計算</h2>
    <div class="inputs">
      <label>
        合格に必要な時間
        <span>
          <input v-model="totalTime" type="number" />
          時間
        </span>
      </label>
      <label>
        平日の勉強時間
        <span>
          <input v-model="weekdayTime" type="number" />
          時間
        </span>
      </label>
      <label>
        休日の勉強時間
        <span>
          <input v-model="holidayTime" type="number" />
          時間
        </span>
      </label>
    </div>
    <div class="results">
      <p>一週間あたりの勉強時間: {{ timePerWeek }}時間</p>
      <p>かかる週数: {{ neededWeeks }}週</p>
      <p>かかる日数: {{ neededDays }}日</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      totalTime: 0,
      weekdayTime: 0,
      holidayTime: 0,
    }
  },
  computed: {
    timePerWeek(): number {
      return this.weekdayTime * 5 + this.holidayTime * 2
    },
    neededWeeks(): number {
      return Math.floor(
        this.hasInvalidInput ? 0 : this.totalTime / this.timePerWeek
      )
    },
    neededDays(): number {
      return this.neededWeeks * 7
    },
    hasInvalidInput(): boolean {
      return this.weekdayTime <= 0 || this.holidayTime <= 0
    },
  },
})
</script>

<style>
.days-calculator {
  padding: 20px;
  max-width: 500px;
  margin: 0 auto;
}

label {
  display: flex;
  justify-content: space-between;
}

label + label {
  margin-top: 8px;
}

input {
  text-align: right;
}
</style>
