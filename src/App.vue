<script setup>
//import chat component
import Chat from "./components/chat/Chat.vue";
import VideoPlayer from "./components/video/VideoPlayer.vue";
import VideoDetails from "./components/video/VideoDetails.vue";

import { ref } from 'vue';

let newDescription = ref("Default description");

const updateVideo = (description) => {
  newDescription.value = description;
};

</script>

<template>
  <div class="tiktok">
    <div>
      <VideoPlayer @update:video-description="updateVideo" />
    </div>
    <div>
      <VideoDetails :description="newDescription" />
      <Chat />
    </div>
  </div>
</template>

<style scoped>
  .tiktok {
    display: grid;
    grid-template-columns: 1fr 1fr;
  }
</style>
