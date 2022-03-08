<template>
  <div id="app">
    <div class="device">
      <h3>Выберите отопительный прибор</h3>
      <div class="grid">
        <p>
        <label for="kamin">Камин</label>
        <input type="radio" id="kamin" value="kamin" v-model="device" />
      </p>

      <p>
        <label for="pech">Печь</label>
        <input type="radio" id="pech" value="pech" v-model="device" />
      </p>

      <p>
        <label for="bana_pech">Банная печь</label>
        <input type="radio" id="bana_pech" value="bana_pech" v-model="device" />
      </p>

      <p>
        <label for="kotel">Котел</label>
        <input type="radio" id="kotel" value="kotel" v-model="device" />
      </p>
      </div>
      
    </div>
    <transition name="fade">
    <div v-show="step > 1" class="fuel">
      <h3>Выберите топливо</h3>
      <div class="grid">
      <p>
        <label for="drova">Дрова, брикеты, пеллеты</label>
        <input type="radio" id="drova" value="drova" v-model="fuel" />
      </p>
      <p v-if="device === 'kamin' || device === 'kotel'">
        <label for="gaz">Газ</label>
        <input type="radio" id="gaz" value="gaz" v-model="fuel" />
      </p>
      <p v-if="device === 'pech' || device === 'kotel'">
        <label for="ugol">Древесный уголь</label>
        <input type="radio" id="ugol" value="ugol" v-model="fuel" />
      </p>
      <p v-if="device === 'kotel'">
        <label for="dizel">Дизельное топливо</label>
        <input type="radio" id="dizel" value="dizel" v-model="fuel" />
      </p>
      </div>
      
    </div>
    </transition>
    <transition name="fade">
    <div v-if="step > 2" class="material">
      <h3>Выберите материалы дымохода</h3>
      <Material-step @choose="compareResult" :fuel="this.fuel"/>
    </div>
    </transition>
    <transition name="fade">
    <div v-if="step > 3" class="configuration">
      <h3>Выберите конфигурацию дымохода</h3>
      <Config-step />
    </div>
    </transition>
  </div>
</template>

<script>
import MaterialStep from './components/MaterialStep.vue';
import ConfigStep from './components/ConfigStep.vue';
export default {
  name: "App",
  components: {
    MaterialStep,
    ConfigStep,
  },
  data() {
    return {
      step: 1,
      device: null,
      fuel: null,
      
      result: {
        material: null
      },
    };
  },
  watch: {    
    device() {
      this.step = 2;
      this.fuel = null;
      this.result.material = null;
    },
    fuel() {
      if(this.fuel) {
        console.log('watch fuel');
        this.step = 3;
      }        
    },
  },
  computed: {
  
  },
  methods: {
    compareResult(obj) {
      if(!this.result.material) {
        this.step = 4;
      }      
      this.result[obj.step] = obj.value;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.grid {
  display: flex;
  justify-content: center;
}
.grid p {
  margin: 0 10px;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
</style>
