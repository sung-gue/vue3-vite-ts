<script setup lang="ts">
import Stomp from "webstomp-client";
import type { Client } from "webstomp-client";
import SockJS from "sockjs-client/dist/sockjs.js";

const host = "http://192.168.10.206:12000";

const serverURL = host + "/stream";
console.log("serverURL", serverURL);
const socket = new SockJS(serverURL);

console.log("socket 1 - ", socket);
const conn = Stomp.over(socket) as Client;
console.log("socket 2 - ", conn);

conn.connect(
  {},
  (frame) => {
    console.log("소켓 연결 성공", frame);
  },
  (error) => {
    console.log("소켓 연결 실패", error);
  }
);

defineProps<{
  msg: string;
}>();
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      You’ve successfully created a project with
      <a target="_blank" href="https://vitejs.dev/">Vite</a> +
      <a target="_blank" href="https://vuejs.org/">Vue 3</a>. What's next?
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
