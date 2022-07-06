<template>
  <div class="hello">
    <p>{{showTimer}}</p>
    <button @click="start">Start</button>
    <button @click="stop">Pauza</button>
    <button @click="reset">Reset</button>
    <p>{{showVuex}}</p>
  </div>
  
</template>

<script>
export default {
  name: 'TimerView',
  data(){
    return{
      h:0,
      m:0,
      s:0,
      interval:null
    }
  },
  methods:{
    start(){
      this.interval = setInterval(()=>{
        this.s +=1

        if(this.s === 60){
          this.m +=1;
          this.s = 0
        }
        if(this.m === 60){
          this.h +=1
          this.m = 0
        }
        if(this.h === 24){
          this.h = 0 
        }
      },1000)
    },
    stop(){
      clearInterval(this.interval)
    },
    reset(){
      this.h = 0
      this.m = 0
      this.s = 0
    }
  },
  computed:{
    showTimer(){
      return `${this.h < 10 ? "0"+this.h : this.h} : ${this.m < 10 ? "0"+this.m : this.m} : ${this.s < 10 ? "0"+this.s : this.s}`
    },
    showVuex(){
      return this.$store.getters.getTest;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
