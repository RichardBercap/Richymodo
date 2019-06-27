<template>
  <div class="main">
   <h1>RichyModo</h1>
   <section class="container">
       <section id="button">
           <button type="button" :disabled="disabled_button" @click="startTime">Start</button>
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
    beforeCreate: function() {
        document.body.className = 'home';
    },
  name: 'Main',
  props: {
    msg: String
  },
  data(){
      return{
          
          time:1,
          seconds:60,
          disabled_button:false,
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
        this.disabled_button = true;
       var interval =   setInterval(()=>{
           
              this.initial_time.seconds--;
              if(this.initial_time.seconds <= 60){
                  
                  this.actual_time.seconds= this.initial_time.seconds;

              }
              if(this.initial_time.seconds < 10){
                  this.actual_time.seconds = `0${this.initial_time.seconds}`;
              }
               if(this.initial_time.minutes < 10){
                  this.actual_time.minutes = `0${this.initial_time.minutes}`;
              }
              if(this.initial_time.seconds == 0){
                  this.initial_time.seconds= 60;
                  this.initial_time.minutes--;
                  this.actual_time.minutes = this.initial_time.minutes;
              }
               if(this.initial_time.minutes < 0){
                   clearInterval(interval);
                   navigator.vibrate(300);
                   
                   this.initial_time = {minutes:this.time,seconds:this.seconds};
                   this.actual_time = {minutes:this.time,seconds:'00'};
                   alert("Time out");
                   this.disabled_button = false;
               }
              //console.log("sdcds");
          },1000);
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    *{
        padding: 0;
        margin: 0;
    }
    .home{
        margin: 0;
        background-color: #1fc8db;
        background-image: linear-gradient(141deg, #1c97df 0%, #1fc8db 51%, #2cb5e8 75%);
        background-repeat: no-repeat;
            width: 100vw;
            height: 100vh;
       background-size: 100% 100%;     
    }
    .main{
             text-align: center;
            margin-top: 5%;
            font-size: 55px;
            color: white;   
    }
    #button{
            text-align: center;
            padding: 10px;
    }
    #button button{
            width: 180px;
            height: 180px;
            border-radius: 50%;
            background: transparent;
            color: white;
            font-size: 35px;
            border-color: white;
            box-shadow: none;
                
            cursor: pointer;
            
    }
    #countdown{
        font-size: 75px;
    }

    @media (width: 600px) {
        body {
            background-image: none;
            
            }
        }
</style>
