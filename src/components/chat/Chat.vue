<script setup>
import { ref, reactive, onMounted } from 'vue';

let message = ref("");

let messages = reactive({
  data: [],
});

onMounted(async () => {
  try {
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
    const data = await response.json();
    data.reverse();
    messages.data = data.slice(0, 10);
    console.log(messages.data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
});

const sendMessage = async () => {
  try {
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        user: "Tibo",
        text: message.value,
      }),
    });

    const data = await response.json();
    console.log(data);

    messages.data.unshift(data);
    message.value = "";
  } catch (error) {
    console.error("Error sending message:", error);
  }
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
