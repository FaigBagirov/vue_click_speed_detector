<template>
  <div>
    <h1>Reaction detector</h1>
      <StartScreen v-show="start"/>
      <ResultScreen v-show="showResult" :theClickSpeed="clickSpeed" :theRankLevel="rankLevel"/>
      <button class="button" ref="playButton" @click="startGame" @mouseover="hoverOn" @mouseleave="hoverOff">Play</button>
      <ClickBox v-show="showBox" @clicked="gameResult"/>
  </div>
  
</template>

<script>
import StartScreen from './components/StartScreen.vue'
import ClickBox from './components/ClickBox.vue'
import ResultScreen from './components/ResultScreen.vue'

export default {
  name: 'App',
  components: {
    StartScreen,
    ClickBox,
    ResultScreen,
  },
  data(){
    return {
      start: true,
      showBox: false,
      showResult: false,
      startTime: 0,
      clickTime: 0,
      clickSpeed: -1,
      rankSpeeds:[350, 300, 250, 200, 150, 100, 50, 10],
      rankLevel: -1,
    }
  },
  methods: {
      hoverOn(){
        this.$refs.playButton.classList.add('btnHovered');
      },
      hoverOff(){
        this.$refs.playButton.classList.remove('btnHovered');
      },
      startGame(){
        this.$refs.playButton.disabled = true;
        this.hoverOff();     

        setTimeout(() => {
          this.showBox = true;
          this.startTime = performance.now();
        },1000);
      },
      calculateRank(startingPoint = 0){
        if (this.clickSpeed > this.rankSpeeds[startingPoint] ){
          this.rankLevel =  startingPoint -1 < 0 ? 0 : startingPoint -1;
        }
        else if (startingPoint > this.rankSpeeds.length){
          this.rankLevel = this.ranks.length-1;
        }
        else{
          startingPoint++;
          this.calculateRank(startingPoint);
        }
      },
      gameResult(){
          this.clickTime = performance.now();
          this.showBox = false;
          this.clickSpeed = Math.floor(this.clickTime - this.startTime);
          this.start = false;
          this.calculateRank();  
          this.showResult = true;
          this.$refs.playButton.disabled = false;
      }
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
}
#app p{
  font-size: 20px;
}
.desc{
  color: green;
  font-size: 16px !important;
  font-style: italic;
}
.button{
  width: 100px;
  height: 39px;
  border-radius: 8px;
  background-color: rgb(174, 255, 174);
  border: 1px solid rgb(136, 255, 136);
  color: #fff;
  font-size: 20px;
  font-weight: 600;
  cursor: pointer;
}

.btnHovered{
  background-color: grey;
  color: #000;
}

button:disabled {
  background-color: rgb(174, 255, 174, 0.5);
  border: 1px solid rgb(136, 255, 136, 0.5);
  color: #fff;
  cursor: default;

}
</style>
