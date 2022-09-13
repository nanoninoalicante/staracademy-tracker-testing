<script setup>
import { useWebSocket } from '@vueuse/core'
import random from "random-words";
const { status, data, send, open, close } = useWebSocket('wss://devproxy.staracademyapp.com/_t-ws-demo')
const sendMessage = () => {
  send(JSON.stringify({ message: random({ exactly: 2, join: '-' }), ts: new Date().toISOString() }))
}
const closeConnection = () => {
  close();
}
const openConnection = () => {
  open();
}
</script>

<template>
  <main>
    <button class="p-4 bg-gray-100 m-2 hover:bg-gray-300" @click="openConnection">open</button>
    <button class="p-4 bg-gray-100 m-2 hover:bg-gray-300" @click="closeConnection">close</button>
    <button class="p-4 bg-gray-100 m-2 hover:bg-gray-300" @click="sendMessage">send</button>
    <p class="break-normal">
      Status: {{ status }}
    </p>
    <p class="break-normal">
      Data: {{ data }}
    </p>
  </main>
</template>
