<script setup>
import { ref, reactive, onMounted } from 'vue';
let message = ref("JUUUUUWWW"); //voor int, string, boolean
let messages = reactive({
  data: ["heel", "even", "testen"]
}); //voor objecten en arrays

const sendMessage = () => {
  messages.data.push(message.value);
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
