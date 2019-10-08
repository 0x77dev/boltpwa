<template>
	<iframe :src="'https://appetize.io/embed/'+appKey+'?device=nexus5&scale='+emuScale+'&autoplay=true&orientation=portrait&deviceColor=black&screenOnly=true'" width="360px" height="640px" frameborder="0" scrolling="no"></iframe>
</template>

<script>
export default {
  name: 'BoltEmulator',
	props: ["appKey", "emuScale"]
}
</script>

<style>
	iframe{
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
	}
</style>