<template>
  <div class="main">
   <h1>RichyModo</h1>
   <section class="container">
       <section id="button">
           <button type="button" @click="startTime">Start</button>
       </section>
       <section id="countdown" >
           {{actual_time.minutes}} : {{actual_time.seconds}}
       </section>
   </section>
  </div>
</template>

<script>
//import { setInterval } from 'timers';
export default {
  name: 'Main',
  props: {
    msg: String
  },
  data(){
      return{
          
          time:5,
          seconds:60,
          initial_time:{
              minutes:this.time,
              seconds:this.seconds
          },
          actual_time:{
              minutes: '25',
              seconds:'00'
          },
      }
  },
  mounted(){
      this.initial_time={
              minutes:this.time,
              seconds:this.seconds
          };
    this.actual_time={
              minutes: this.time,
              seconds:'00'
          };
  },
  methods:{
      startTime(){
        
       var interval =   setInterval(()=>{
              this.initial_time.seconds--;
              if(this.initial_time.seconds <= 60){
                  
                  this.actual_time.seconds= this.initial_time.seconds;

              }
              if(this.initial_time.seconds < 10){
                  this.actual_time.seconds = `0${this.initial_time.seconds}`;
              }
              if(this.initial_time.seconds == 0){
                  this.initial_time.seconds= 60;
                  this.initial_time.minutes--;
                  this.actual_time.minutes = this.initial_time.minutes;
              }
               if(this.initial_time.seconds == 0 && this.initial_time.minutes == 0){
                   clearInterval(interval);
                   this.initial_time = {minutes:this.time,seconds:this.seconds};
                   this.actual_time = {minutes:this.time,seconds:'00'};
               }
              //console.log("sdcds");
          },1000);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
