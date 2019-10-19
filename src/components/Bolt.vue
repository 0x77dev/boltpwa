<template>
  <div id="emulator">
    <iframe
      :src="'https://appetize.io/embed/'+appKey+'?device=nexus5&scale='+emuScale+'&autoplay=true&orientation=portrait&deviceColor=black&screenOnly=true'"
      frameborder="0"
      scrolling="no"
    ></iframe>
    <br />
  </div>
</template>

<script>
import * as Controller from "@/controller";
export default {
  name: "BoltEmulator",
  props: ["appKey", "emuScale"],
  mounted() {
    // Keep Alive
    setInterval(() => {
      Controller.heartbeat();
    }, 5000);
  }
};
</script>

<style scoped>
#emulator {
  margin: 0;
  z-index: 1000;
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: black;
}
iframe, iframe:not(.md-image) {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
  border: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  z-index: 999999;
}
</style>