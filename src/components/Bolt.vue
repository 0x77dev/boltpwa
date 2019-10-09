<template>
	<div>
		<iframe :src="'https://appetize.io/embed/'+appKey+'?device=nexus5&scale='+emuScale+'&autoplay=true&orientation=portrait&deviceColor=black&screenOnly=true'" width="360px" height="640px" frameborder="0" scrolling="no"></iframe>
		<br> <img id="screenshot">
	</div>
</template>

<script>
import * as Controller from "@/controller";
export default {
	name: 'BoltEmulator',
	props: ["appKey", "emuScale"],
	mounted(){
	  // Keep Alive
	  setInterval(()=>{
		  Controller.heartbeat();
	  }, 5000);
	}
};
</script>

<style>
	iframe{
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
	}
</style>