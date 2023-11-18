<script setup>
import { ref, reactive, onMounted } from 'vue';

let message = ref("JUUUUUWWW");

let messages = reactive({
  data: [],
});

onMounted(async () => {
  try {
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
    const data = await response.json();
    messages.data = data.slice(-10);
    console.log(messages.data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});

const sendMessage = () => {
  messages.data.unshift(message.value);
  message.value = "";
};
</script>

<template>
  <div>
    <ul>
      <li v-for="m in messages.data">
        <strong>{{ m.user }}:</strong> {{ m.text }}
      </li>
    </ul>
  </div>
  <div>
    <input v-model="message" type="text" placeholder="">
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped></style>
