<script setup>
import { useWebSocket } from "@vueuse/core";
import random from "random-words";
import { useAxios } from "@vueuse/integrations/useAxios";
const { status, data, send, open, close } = useWebSocket(
  "wss://devproxy.staracademyapp.com/_t-ws-demo"
);
const sendMessage = () => {
  send(
    JSON.stringify({
      message: random({ exactly: 2, join: "-" }),
      ts: new Date().toISOString(),
    })
  );
};
const closeConnection = () => {
  close();
};
const openConnection = () => {
  open();
};
const forceError = () => {
  throw new Error("testing sentry through a proxy");
};
const forceErrorFromHttp = async () => {
  await fetch("https://webhook.site/bc78d3f2-2604-44be-8153-503b29797fda", {
    method: "post",
    body: "hello world",
  }).then(async (response) => {
    if (!response.ok) {
      console.log("error: ", await response.text());
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  });
};
const forceErrorFromHttpUnhandled = async () => {
  await fetch("https://webhook.site/bc78d3f2-2604-44be-8153-503b29797fda", {
    method: "post",
    body: "hello world",
  });
  const { data, isFinished } = await useAxios(
    "https://webhook.site/bc78d3f2-2604-44be-8153-503b29797fda",
    { method: "post" }
  );
  console.log("response: ", data);
};
</script>

<template>
  <main>
    <button
      class="p-4 bg-gray-100 m-2 hover:bg-gray-300"
      @click="openConnection"
    >
      open
    </button>
    <button
      class="p-4 bg-gray-100 m-2 hover:bg-gray-300"
      @click="closeConnection"
    >
      close
    </button>
    <button class="p-4 bg-gray-100 m-2 hover:bg-gray-300" @click="sendMessage">
      send
    </button>
    <button class="p-4 bg-gray-100 m-2 hover:bg-gray-300" @click="forceError">
      Force Error
    </button>
    <button
      class="p-4 bg-gray-100 m-2 hover:bg-gray-300"
      @click="forceErrorFromHttp"
    >
      Force error from http
    </button>
    <button
      class="p-4 bg-gray-100 m-2 hover:bg-gray-300"
      @click="forceErrorFromHttpUnhandled"
    >
      Force error from http unhandled
    </button>
    <p class="break-normal">Status: {{ status }}</p>
    <p class="break-normal">Data: {{ data }}</p>
  </main>
</template>
