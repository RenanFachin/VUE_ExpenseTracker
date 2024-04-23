<script setup>
import { useToast } from '@/components/ui/toast/use-toast'
import { ref } from 'vue'

const text = ref('')
const amount = ref('')

const { toast } = useToast()

function handleSubmit() {
  console.log(text.value, amount.value)

  toast({
    title: 'Scheduled: Catch up',
    description: 'Friday, February 10, 2023 at 5:57 PM',
  });
}
</script>

<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="handleSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount">Amount <br />
        (negative - expense, positive - income)</label>
      <input type="text" id="amount" placeholder="Enter amount..." v-model="amount" />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>