<template>
  <div id="app">
		<div v-if="!isSetupComplete" class="setup">
			<h2>Select Emulator:</h2>
			<select v-model="appKey">
				<option v-for="(item, key) in keys" :value="item">
					{{item}}
				</option>
			</select>
			<br>
			<h2>Scale:</h2>
			<label>
				{{ scale }}
				<input type="range" v-model="scale" min="25" step="5" max="100">
			</label>
			<br>q
			<button class="setupDone" @click="isSetupComplete = true">Start</button>
		</div>
		<Bolt v-if="isSetupComplete" :emu-scale="scale" :app-key="appKey" />
  </div>
</template>

<script>
import Bolt from './components/Bolt.vue'
export default {
  name: 'app',
  components: {
    Bolt
  },
  data(){
		let keys = ["4azm1g3dvhttajdpe8qtxkrhd8", "cnh02d4hmfu2j4wzuzp5tgnur8", "69cpmrbarxm1tnc0qx865t35v8", "87e1ugzuwce418z5mqc11e4y70", "95upmthqmh71820gwhq1nquq8c", "vr4jgrdxq7hxaqdnwgfynwuv0m"];

	  let shuffle = (a) => {
		  for (let i = a.length - 1; i > 0; i--) {
			  const j = Math.floor(Math.random() * (i + 1));
			  [a[i], a[j]] = [a[j], a[i]];
		  }
		  return a;
	  };

  	return {
  		keys,
  		appKey:	shuffle(keys)[0],
			isSetupComplete: false,
			scale: 100
		}
		}
}
</script>

<style>
	div.setup{
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		padding: 50px;
	}
#app {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
	overflow: hidden;
}
	button.setupDone{
		border: 1px solid black;
		font-size: medium;
		margin-top: 20px;
	}
</style>
