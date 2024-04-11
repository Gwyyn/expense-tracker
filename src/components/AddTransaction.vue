<template>
  <h3 style="margin-top: 15px">
    Add new transaction
  </h3>
  <n-form>
    <n-space vertical>
      <n-form-item label="Text">
        <label>Text</label>
        <n-input round placeholder="Input text"
                 type="text"
                 v-model:value="text"
        />
      </n-form-item>
      <n-form-item label="Amount">
        <label>
          Amount
          (negative - expense, positive - income)
        </label>
        <n-input
            v-model:value="amount"
            round placeholder="Input amount...">
          <template #suffix>
            $
          </template>
        </n-input>
      </n-form-item>
      <n-form-item>
        <n-button type="success" @click="onSubmitForm">
          Add transaction
        </n-button>
      </n-form-item>
    </n-space>
  </n-form>
</template>

<script setup>
import {ref, defineEmits} from 'vue'
import {NForm, NButton, NInput, NSpace} from 'naive-ui'
import {useToast} from "vue-toastification";


const text = ref('')
const amount = ref('')

const emit = defineEmits(['transactionSubmitted'])

const toast = useToast()

const onSubmitForm = () => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled');
    return
  }
  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
    showPromptIcons: false,
  }

  emit('transactionSubmitted', transactionData)

  text.value = '';
  amount.value = '';
}

</script>

<style scoped>
label {
  margin-left: 10px;
}

</style>