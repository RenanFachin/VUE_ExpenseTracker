<script setup>
import { ref, computed } from 'vue';

// Componentes
import Balance from '@/components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue'
import TransactionList from '@/components/TransactionList.vue'
import AddTransaction from '@/components/AddTransaction.vue'
import Toaster from '@/components/ui/toast/Toaster.vue'


// Utils
// tudo que for reativo devemos utilizar ref

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 419.99 },
  { id: 3, text: 'Book', amount: -39 },
  { id: 4, text: 'Book', amount: -10.10 },
])

// Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

// Filtrar pelo tipo de receita e após fazer um somatório
// Get Income -> filter + reduce
const totalIncome = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
})

// Get Expenses -> filter + reduce
const totalExpenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0).toFixed(2)
})
</script>

<template>
  <div class="container" >
    <Balance :total="total" />
    <IncomeExpenses :income="Number(totalIncome)" :expenses="Number(totalExpenses)" />
    <TransactionList :allTransactions="transactions" />
    <AddTransaction />
  </div>

  <Toaster />
</template>