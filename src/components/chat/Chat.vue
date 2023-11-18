<script setup>
import { ref, reactive, onMounted } from 'vue';

let message = ref("JUUUUUWWW");
let messages = reactive({
  data: [],
});

// fetch messages from this api url: https://lab5-p379.onrender.com/api/v1/messages/
fetch("https://lab5-p379.onrender.com/api/v1/messages/")
  .then((res) => res.json())
  .then((data) => {
    data.reverse();

    // Use slice to get the first 10 messages
    let first10Messages = data.slice(0, 10);

    // Use map to extract the "text" property from each object
    messages.data = first10Messages.map((message) => message.text);

    console.log(messages); // This will log the correct data
  });

const sendMessage = () => {
  messages.data.unshift(message.value);
  message.value = "";
};
</script>

<template>
  <div>
    <ul>
      <li v-for="m in messages.data">{{ m }}</li>
    </ul>
  </div>
  <div>
    <input v-model="message" type="text" placeholder="">
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped></style>
