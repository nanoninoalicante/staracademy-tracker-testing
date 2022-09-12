<script setup>
import TheWelcome from '@/components/TheWelcome.vue'
import { useWebSocket } from '@vueuse/core'
const { status, data, send, open, close } = useWebSocket('ws://websocket')
const sendMessage = () => {
  send(JSON.stringify({ message: "message"}))
}
const closeConnection = () => {
  close();
}
</script>

<template>
  <main>
    <button @click="closeConnection">close</button>
    <button @click="sendMessage">send</button>
    <pre>
          Status: {{ status }}
          Data: {{ data }}
      </pre>
  </main>
</template>
