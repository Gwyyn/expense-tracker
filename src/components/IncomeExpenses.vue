<template>
  <div class="inc-exp-container">
    <div>
      <h4>INCOME</h4>
      <p class="money-plus">+{{ income }}$</p>
    </div>
    <div class="vertical-divider"></div>
    <div>
      <h4>EXPENSE</h4>
      <p class="money-minus">{{ expenses }}$</p>
    </div>
  </div>
</template>

<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  }
})

</script>

<style scoped>
.inc-exp-container {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  align-items: center;
  background-color: white;
  min-width: 300px;
  min-height: 100px;
  padding: 10px;
  border-radius: 10px;
  box-shadow: black;
}

.vertical-divider {
  width: 1px;
  min-height: 80px;
  border-left: 1px solid #494747;
}

.money-plus {
  color: #04a904;
  font-weight: bold;
}

.money-minus {
  color: #c90a0a;
  font-weight: bold;
}
</style>