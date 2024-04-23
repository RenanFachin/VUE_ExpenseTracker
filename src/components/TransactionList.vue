<script setup>
// defineProps é utilizado para receber propriedades entre componentes
import { defineProps } from 'vue'

const props = defineProps({
  allTransactions: {
    type: Array,
    required: true
  }
})

// Custom event
const emit = defineEmits(['transactionDeleted'])

function handleDeleteTransaction(id){
  emit('transactionDeleted', id)
}

</script>


<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li v-for="transaction in allTransactions" v-bind:key="transaction.id"
      v-bind:class="transaction.amount < 0 ? 'minus' : 'plus'">
      {{ transaction.text }}

      <span>$ {{ transaction.amount }}</span>
      <button class="delete-btn" @click="handleDeleteTransaction(transaction.id)">x</button>
    </li>
  </ul>
</template>