<script setup>
import { ref, computed } from 'vue';
import { useToast } from '@/components/ui/toast/use-toast'
const { toast } = useToast()

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

function generateUniqueId() {
  return Math.floor(Math.random() * 10000)
}

// ADD transaction
function handleTransactionSubmitted(data) {
  const { text, amount } = data

  transactions.value.push({
    id: generateUniqueId(),
    text: text,
    amount: amount
  })

  toast({
    description: `Transaction ${text} of value ${amount} was registered successfully`
  })

}

// Delete transaction
function handleTransactionDeleted(id) {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)

  toast({
    description: `Transaction deleted`
  })
}
</script>

<template>
  <div class="container">
    <Balance :total="Number(total)" />
    <IncomeExpenses :income="Number(totalIncome)" :expenses="Number(totalExpenses)" />
    <TransactionList :allTransactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transcationSubmitted="handleTransactionSubmitted" />
  </div>

  <Toaster />
</template>