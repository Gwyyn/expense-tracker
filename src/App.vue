<template>
  <Header/>
  <Balance :total="total"/>
  <IncomeExpenses :income="+income" :expenses="+expenses"/>
  <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
  <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'
import {ref, computed, onMounted} from 'vue'
import {useToast} from "vue-toastification";

const toast = useToast()

const transactions = ref([]);

onMounted(() => {
  const saveTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (saveTransactions) {
    transactions.value = saveTransactions
  }
})

//get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
})

//get income
const income = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
})

//get expenses
const expenses = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
})

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: (Date.now().toString()),
    text: transactionData.text,
    amount: transactionData.amount,
  })

  saveTransactionsToLocalStorage();

  toast.success('Transaction added')
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted')
}

const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>

<style lang="scss">

</style>