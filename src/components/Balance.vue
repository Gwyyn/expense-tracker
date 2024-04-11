<template>
  <h4>YOUR BALANCE</h4>
  <div class="total">{{ total }}$</div>
</template>

<script setup>
import {defineProps} from 'vue';

const props = defineProps({
  total: {
    type: Number,
    required: true,
  }
})
</script>

<style scoped>

.total {
  font-size: 30px;
  font-weight: bold;
  margin-bottom: 10px;
}

</style>