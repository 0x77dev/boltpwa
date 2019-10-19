<template>
  <div id="app" class="page-container">
    <md-app md-mode="reveal" style="margin-bottom: 0;">
      <md-app-toolbar class="md-primary">
        <span class="md-title">Bolt Emulator</span>
      </md-app-toolbar>

      <md-app-content>
        <div v-if="keys === null">
          <md-empty-state
            md-rounded
            md-icon="access_time"
            md-label="Loading..."
            md-description="Wait please, if it not loads please check internet connection"
          ></md-empty-state>
        </div>
        <div v-if="!isSetupComplete && keys !== null" class="setup">
          <md-steppers md-vertical>
            <md-step
              md-icon="phone"
              id="first"
              md-label="Select Emulator:"
              md-description="Optional"
            >
              <md-field>
                <md-select
                  v-model="appKey"
                  name="emulator"
                  id="emuselect"
                  placeholder="Select Emulator Key"
                >
                  <md-option v-for="(item, key) in keys" :key="key" :value="item">{{key}}:{{item}}</md-option>
                </md-select>
              </md-field>
            </md-step>
            <md-step md-label="Own Appetize.io key" md-description="Optional">
              <md-field>
                <label>My own key</label>
                <md-input v-model="appKey" :placeholder="appKey"></md-input>
              </md-field>
            </md-step>
            <md-step id="second" md-label="Set Scale:" md-description="Optional">
              Scale: {{ scale }}
              <br />
              <input type="range" min="75" max="125" step="5" v-model="scale"> 
            </md-step>

            <md-step @click="isSetupComplete = true" id="third" md-label="Start">
              <md-button class="setupDone" @click="isSetupComplete = true">Start</md-button>
            </md-step>
          </md-steppers>
        </div>
      </md-app-content>
    </md-app>
	<Bolt v-if="isSetupComplete" :emu-scale="scale" :app-key="appKey" />
  </div>
</template>

<script>
import Bolt from "./components/Bolt.vue";
import axios from "axios";

export default {
  name: "app",
  components: {
    Bolt
  },
  data() {
    return {
      isSetupComplete: false,
      appKey: null,
      keys: null,
      scale: 100
    };
  },
  watch: {
    scale(newScale) {
      localStorage.scale = newScale;
	},
	appKey(newAppKey){
		localStorage.appKey = newAppKey;
	}
  },
  mounted() {
    if (localStorage.scale) {
      this.scale = localStorage.scale;
	}
	if (localStorage.appKey) {
      this.appKey = localStorage.appKey;
    }
    axios
      .get("https://my-json-server.typicode.com/0x77dev/bolt.keys/db")
      .then(response => {
        this.keys = response.data.keys;
        this.appKey = response.data.keys[0];
      });
  }
};
</script>
<style scoped>
#emulator{
	margin: 0;
}
#app > div.md-app.md-app-side-drawer.md-layout-row.md-reveal.md-theme-default > main > div.md-app-scroller.md-layout-column.md-flex.md-theme-default.md-scrollbar > div{
	margin: 0;
}

.range {
  -webkit-appearance: none;
  -moz-appearance: none;
  position: absolute;
  left: 50%;
  top: 50%;
  width: 200px;
  margin-top: 10px;
  transform: translate(-50%, -50%);
}

input[type=range]::-webkit-slider-runnable-track {
  -webkit-appearance: none;
  background: rgba(59,173,227,1);
  background: -moz-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -webkit-gradient(left bottom, right top, color-stop(0%, rgba(59,173,227,1)), color-stop(25%, rgba(87,111,230,1)), color-stop(51%, rgba(152,68,183,1)), color-stop(100%, rgba(255,53,127,1)));
  background: -webkit-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -o-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -ms-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#3bade3 ', endColorstr='#ff357f ', GradientType=1 );
  height: 2px;
}

input[type=range]:focus {
  outline: none;
}

input[type=range]::-moz-range-track {
  -moz-appearance: none;
  background: rgba(59,173,227,1);
  background: -moz-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -webkit-gradient(left bottom, right top, color-stop(0%, rgba(59,173,227,1)), color-stop(25%, rgba(87,111,230,1)), color-stop(51%, rgba(152,68,183,1)), color-stop(100%, rgba(255,53,127,1)));
  background: -webkit-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -o-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: -ms-linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  background: linear-gradient(45deg, rgba(59,173,227,1) 0%, rgba(87,111,230,1) 25%, rgba(152,68,183,1) 51%, rgba(255,53,127,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#3bade3 ', endColorstr='#ff357f ', GradientType=1 );
  height: 2px;
}

input[type=range]::-webkit-slider-thumb {
  -webkit-appearance: none;
  border: 2px solid;
  border-radius: 50%;
  height: 25px;
  width: 25px;
  max-width: 80px;
  position: relative;
  bottom: 11px;
  background-color: #1d1c25;
  cursor: -webkit-grab;

  -webkit-transition: border 1000ms ease;
  transition: border 1000ms ease;
}

input[type=range]::-moz-range-thumb {
  -moz-appearance: none;
  border: 2px solid;
  border-radius: 50%;
  height: 25px;
  width: 25px;
  max-width: 80px;
  position: relative;
  bottom: 11px;
  background-color: #1d1c25;
  cursor: -moz-grab;
  -moz-transition: border 1000ms ease;
  transition: border 1000ms ease;
}



.range.blue::-webkit-slider-thumb {
   border-color: rgb(59,173,227);
}

.range.ltpurple::-webkit-slider-thumb {
   border-color: rgb(87,111,230);
}

.range.purple::-webkit-slider-thumb {
   border-color: rgb(152,68,183);
}

.range.pink::-webkit-slider-thumb {
   border-color: rgb(255,53,127);
}

.range.blue::-moz-range-thumb {
   border-color: rgb(59,173,227);
}

.range.ltpurple::-moz-range-thumb {
   border-color: rgb(87,111,230);
}

.range.purple::-moz-range-thumb {
   border-color: rgb(152,68,183);
}

.range.pink::-moz-range-thumb {
   border-color: rgb(255,53,127);
}

input[type=range]::-webkit-slider-thumb:active {
  cursor: -webkit-grabbing;
}

input[type=range]::-moz-range-thumb:active {
  cursor: -moz-grabbing;
}
</style>