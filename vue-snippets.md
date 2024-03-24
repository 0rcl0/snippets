```vue
<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";
let currentTime = ref(0);
let videoPlayer = ref();
let finished = ref(false);
onMounted(() => {
  // send message to background and set learn process;

  if (videoPlayer.value) {
    videoPlayer.value.currentTime = 3000 / 1000;
  }

  videoPlayer.value.addEventListener("timeupdate", (e) => {
    let process = Math.floor(e.target.currentTime);
    if (currentTime.value < process) {
      currentTime.value = process;
    }
  });

  videoPlayer.value.addEventListener("");

  videoPlayer.value.addEventListener("ended", (e) => {
    console.log("video play finished");
    finished.value = true;
    // send message to background and update learn status is finished
  });
});

onBeforeUnmount(() => {});
</script>

<template>
  <video
    ref="videoPlayer"
    id="video"
    controls
    controlslist="disableplayback noplaybackrate noseek"
    muted
  >
    <source src="./assets/learn-video.mp4" type="video/mp4" />
  </video>
</template>

<style scoped>
#video {
  width: 80%;
  height: 80%;
}

/* video::-webkit-media-controls-timeline {
  display: none;
} */
</style>
```
