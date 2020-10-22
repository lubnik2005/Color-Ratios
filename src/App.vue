<template>
  <div id="app">
    <div class="sidebar left-sidebar nes-container" >
        <button type="button" @click="add('firstColorVolume',number,0)" :class="['nes-btn', 'is-error']" v-for="number in binaryList" :key="number + 'addRed'" v-text="'+' + number * 2 + ' Red'"></button>
        <button type="button" @click="sub('firstColorVolume',number,0)" :class="['nes-btn', 'is-error']" v-for="number in binaryList" :key="number + 'subRed'" v-text="'-' + number * 2 + ' Red'"></button>
        <button type="button" @click="add('secondColorVolume',number,0)" :class="['nes-btn', 'is-success']" v-for="number in binaryList" :key="number + 'addGreen'" v-text="'+' + number * 2 + ' Green'"></button>
        <button type="button" @click="sub('secondColorVolume',number,0)" :class="['nes-btn', 'is-success']" v-for="number in binaryList" :key="number + 'subGren'" v-text="'-' + number * 2+ ' Green'"></button>

    </div>
    <div class="canvas nes-container with-title is-centered">
      <p class="title">Color Ratios </p>
      <img src="./assets/table.svg" class="table" />
      <beaker :firstColorVolume="beakers[0].firstColorVolume" :secondColorVolume="beakers[0].secondColorVolume" :bubbles="bubbles" />
      <beaker :firstColorVolume="beakers[1].firstColorVolume" :secondColorVolume="beakers[1].secondColorVolume" :bubbles="bubbles" />
      <button type="button" id="reset" @click="reset()" :class="['nes-btn', 'is-primary']" v-text="'Reset'" />
    </div>
    <div class="sidebar right-sidebar nes-container" >
        <button type="button" @click="add('firstColorVolume',number,1)" :class="['nes-btn', 'is-error']" v-for="number in binaryList" :key="number + 'addRed'" v-text="'+' + number * 2 + ' Red'"></button>
        <button type="button" @click="sub('firstColorVolume',number,1)" :class="['nes-btn', 'is-error']" v-for="number in binaryList" :key="number + 'subRed'" v-text="'-' + number * 2 + ' Red'"></button>
        <button type="button" @click="add('secondColorVolume',number,1)" :class="['nes-btn', 'is-success']" v-for="number in binaryList" :key="number + 'addGreen'" v-text="'+' + number * 2 + ' Green'"></button>
        <button type="button" @click="sub('secondColorVolume',number,1)" :class="['nes-btn', 'is-success']" v-for="number in binaryList" :key="number + 'subGren'" v-text="'-' + number * 2 + ' Green'"></button>
    </div>
  </div>
</template>

<script>
import Beaker from './components/Beaker.vue';
export default {
  name: 'App',
  methods: {
    reset(){
      for (let key in this.beakers){
        for (let childKey in this.beakers[key]){
          this.beakers[key][childKey] = 0;
        }
      }
    },
    add(color,number,beaker){
      console.log(number);
      console.log(this.beakers);
      if (this.beakers[beaker].firstColorVolume + this.beakers[beaker].secondColorVolume + number <= 250){
        console.log('added');
        this.beakers[beaker][color] +=number;
        console.log('added');
      }
    },
    sub(color,number,beaker){
      if (this.beakers[beaker][color] - number >= 0){
        this.beakers[beaker][color] -= number
      }
    }
  },
  data: function(){
    return({
      binaryList: [ // Must be half since pixels are doubled
        1, 5, 10
      ], 
      beakers: [
        {
          firstColorVolume:0,
          secondColorVolume: 0,
        },
        {
          firstColorVolume:0,
          secondColorVolume: 0,
        }
      ],
      bubbles: 10
    })
  },
  components: {
    Beaker
  }
}
</script>

<style lang="scss">

  #app {
    position:relative;
    top: 10px;
  }

  .nes-btn {
    width: 170px;
    text-transform: capitalize;

  }

  #reset {
    z-index: 12;
    position: relative;
    top: 80px;
  }
  .table {
    width: 800px;
    position: absolute;
    bottom: -16px;
    left: -20px;
    z-index: 3;
  }

  .canvas {
    position: absolute;
    top: 0px;
    left : 250px;
    background-color:lightblue;
    width: 780px;
    height: 700px;
  }

  .sidebar {
    position: absolute;
    top: 0px;
    width: 250px;
    height: 700px;
    background:linear-gradient(to bottom, #e1a6fc 0%, #cd6bfa 100%);
  }

  .right-sidebar {
    position: absolute;
    left:1030px
  }
</style>
