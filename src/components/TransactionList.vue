<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  allTransactions: {
    type: Array,
    required: true
  }
})
</script>


<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li v-for="transaction in allTransactions" v-bind:key="transaction.id"
      v-bind:class="transaction.amount < 0 ? 'minus' : 'plus'">
      {{ transaction.text }}

      <span>$ {{ transaction.amount }}</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>