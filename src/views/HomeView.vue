<script setup>
import TheWelcome from '@/components/TheWelcome.vue'
import { useWebSocket } from '@vueuse/core'
const { status, data, send, open, close } = useWebSocket('wss://devproxy.staracademyapp.com/_t-ws-demo?api_key=VCXCEuvhGcBDP7XhiJJUDvR1e1D3eiVjgZ9VRiaV&notify_self')
const sendMessage = () => {
  send(JSON.stringify({ message: "message"}))
}
const closeConnection = () => {
  close();
}
</script>

<template>
  <main>
    <button classs="p-4 bg-gray-100" @click="closeConnection">close</button>
    <button classs="p-4 bg-gray-100" @click="sendMessage">send</button>
    <pre>
          Status: {{ status }}
          Data: {{ data }}
      </pre>
  </main>
</template>
