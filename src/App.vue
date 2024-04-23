<script setup>
import { ref, computed } from 'vue';

// Compponentes
import Header from '@/components/Header.vue'
import Balance from '@/components/Balance.vue'
import IncomeExpenses from '@/components/IncomeExpenses.vue';
import TransactionList from '@/components/TransactionList.vue';
import AddTransaction from '@/components/AddTransaction.vue';

// Utils
// tudo que for reativo devemos utilizar ref

const transactions = ref([
  { id: 1, text: 'Flower', amount: -19.99 },
  { id: 2, text: 'Salary', amount: 419.99 },
  { id: 3, text: 'Book', amount: -39 },
  { id: 4, text: 'Book', amount: -10.10 },
])

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})


</script>

<template>
  <Header />

  <div class="container">
    <Balance :total="total"/>
    <IncomeExpenses />
    <TransactionList :allTransactions="transactions"/>
    <AddTransaction />
  </div>
</template>