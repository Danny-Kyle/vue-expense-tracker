<script setup>
import { ref, computed } from 'vue'
import AddTransaction from './components/AddTransaction.vue'
import Header from './components/Header.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TotalBalance from './components/TotalBalance.vue'
import TransactionList from './components/TransactionList.vue'

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 299.94 },
  { id: 3, text: 'Book', amount: -10 },
  { id: 4, text: 'Camera', amount: 150 }
])

//to get total balance
const totalBalance = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

//to get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

//to get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})
</script>

<template>
  <Header />
  <div class="container">
    <TotalBalance :totalBalance="totalBalance" />
    <IncomeExpenses :expenses="expenses" :income="income" />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<!-- older method
<script>
import Header from './components/Header.vue'

export default {
  components: {
    Header,
    TotalBalance,
    IncomeExpenses,
    AddTransaction, 
    TransactionList
  }
}

</script> -->
