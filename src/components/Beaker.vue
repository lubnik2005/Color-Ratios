<template>
    <div class="beaker">    
        <unit v-for="unit in divisions" :key="unit" v-bind:unit="unit" v-bind:number="(divisions + 1 - unit) * 20" />
        <div 
            class="liquid"
            :style="
                'height:' + totalVolume + 'px;' +
                'background-color: rgb( ' + firstColorRatio + ',' + secondColorRatio + ', 0)'
            "
            >
                    <div class="bubble" v-for="(bubble,index) in bubbles" :key="index" />
        </div>
        <div class="colorVolumes">
            <div>Red:<span v-text="firstColorVolume * 2" />mL</div>
            <div>Green:<span v-text="secondColorVolume * 2" />mL</div>
        </div>
    </div>
</template>
<script>
import Unit from './Unit.vue';
export default {
    name: 'Beaker',
    data: function(){
        return({
            divisions: 25,
            brightness: 300

        })
    },
    components: {
        Unit
    },
    computed: {
        firstColorRatio(){
            return(this.brightness * this.firstColorVolume/this.totalVolume);
        },
        secondColorRatio(){
            return(this.brightness * this.secondColorVolume/this.totalVolume);
        },
        totalVolume: function(){
            return((this.firstColorVolume + this.secondColorVolume) * 2)
        }
    },
    props: [
        'firstColorVolume', 'secondColorVolume','bubbles'
    ]
}
</script>
<style scoped lang="scss">
    .beaker {
        backdrop-filter: blur(2px);
        margin-right: 10px;
        bottom: -30px;
        display: inline-block;
        z-index: 4;
        position:relative;
        width: 300px;
        height: 520px;
        background-color:none;
        border-style: solid;
        border-radius: 0% 0% 20% 20% / 0% 0% 10% 10%;
        border-top: none;
        overflow: hidden;

    }
    
    .colorVolumes {
        text-align: left;
        position: absolute;
        bottom: 30px;
        left: 20px;
        z-index: 10;
    }

    .liquid {
        z-index: 5;
        position:absolute;
        bottom: 0px;
        width: 100%;
        overflow: hidden;
        transition: height 0.5s ease-out;
    }

    .liquid:after {
    background-color: rgba(255, 255, 255, 0.25);
    bottom: -10px;
    content: '';
    height: 200%;
    left: 0px;
    position: absolute;
    transform: rotate(30deg);
    -webkit-transform: rotate(15deg);
    width: 110px;
    }

.bubble {
  position: absolute;
  animation-name: bubble;
  animation-iteration-count: infinite;
  animation-timing-function: linear;
  background-color: rgba(255, 255, 255, 0.2);
  bottom: 20px;
  border-radius: 10px;
  height: 20px;
  width: 20px;
}

@keyframes bubble {
  0% { bottom: 10px; }

   50% {
     background-color: rgba(255, 255, 255, 0.2);
      bottom: 40%;
   }

   100% {
     background-color: rgba(255, 255, 255, 0);
      bottom: 90%;
   }
}

@for $i from 1 through 100 {
  .bubble:nth-child(#{$i}) {
    left: random(98) * 1%;
    animation-delay: random() * 30ms;
    animation-duration: (random(10) + 3) * 500ms;
    transform: scale((random(10) + 3)/10);
  }
}
</style>