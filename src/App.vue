<template>
  <div id="app">
      <div class="App-buttons">
        <button @click="isUp = 'increase'" :disabled="water === 100"> increaseWaterLevel </button>
        <button @click="isUp = 'decrease'" :disabled="water === 0"> decreaseWaterLevel </button>
      </div>
      <span class='bathtub-description'>Water Level: {{water}}%</span>
      <span class='bathtub-description'>{{isUp}}</span>
      <div class='bathtub'>
        <div class='bathtub__body'>
          <!-- <div class='bathtub__111' ></div>  -->
        <div :style="{background: 'aqua', height: waterLevel, width: '100%'}"></div>
        </div>
      </div>
  </div>
</template>

<script>


export default {
  name: 'App',
 data() {
    return {
      water: 0,
      isUp: '',
      interval: '',
    };
  },

  computed: {
    waterLevel() {
      return `${this.water}%`;
    }
  },

  methods: {
    change() {
      this.interval = setTimeout(() => {
        if (this.isUp === 'increase' && this.water < 100) {
          console.log('>>>');
          this.water += 20;
        }
        if (this.isUp === 'decrease' && this.water > 0) {
          console.log('<<<');
          this.water -= 20;
        }}, 2000)   
    },
  },

  watch: {
    isUp(){
      clearTimeout(this.interval);
      this.change();
    },
    water(){
      this.change()
    },
  },



  beforeDestroy() {
   clearTimeout(this.interval);
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 400px;
  height: 400px;
  margin: 10px auto;
  border: 5px solid black;

  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}

button {
  width: 150px;
  height: 50px;
  margin: 10px;
}

.App-buttons {
  display: flex;
  justify-content: space-around;
}

.bathtub-description {
  display: block;
}

.bathtub__body {
  width: 100px;
  height: 200px;
  border: 5px solid cadetblue;
  border-radius: 10px;
  display: flex; 
  align-items: end;
}

.bathtub__111 {

}
</style>
