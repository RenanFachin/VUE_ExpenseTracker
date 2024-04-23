<script setup>
import { useToast } from '@/components/ui/toast/use-toast'
import { ref } from 'vue'

const text = ref('')
const amount = ref('')

// Criando um evento custom para sinalizar
const emit = defineEmits(['transcationSubmitted'])

const { toast } = useToast()

function handleSubmit() {
  if (!text.value || !amount.value) {
    return toast({
      variant: 'destructive',
      title: 'Both fields must be filled',
    });
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }

  // Chamando o custom event
  emit('transcationSubmitted', transactionData)
  
  text.value = ''
  amount.value = ''
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