<template>
  <div id='app' v-bind:class="typeof weather.main !='undefined' && weather.main.temp>20 ? 'warm':''">
     <main>
       <div class="search-box">
         <input type="text" name="" id="" class="search-bar" placeholder="Enter the city here....." v-model="query" v-on:keypress="fetchWeather"/>
       </div>
       <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
         <div class="location-box">
           <div class="location">{{weather.name}},{{ weather.sys.country}}</div>
           <div class="date">{{ dateBuilder() }}</div>

         </div>
         <div class="weather-box">
           <div class="temp">{{ Math.round(weather.main.temp)}}°C</div>
           <div class="weather">{{ weather.weather[0].main}}</div>
           <div class="pressure">Pressure: {{ weather.main.pressure}} Pa</div><br>
           <div class="humidity">Humidity: {{ weather.main.humidity}}%</div>
         </div>
         <div class="element"></div>
       </div>
     </main>
  </div>
</template>

<script>


export default {
 name:'app',
 data() {
  return {
      api_key:'a003634552d8204b115d0beb72c8e7a7',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}

  }
 },
 methods:{
     fetchWeather:function(e){
      if(e.key == 'Enter'){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`).then(res => {
          return res.json();
        }).then(this.setResults);
        
        
      }
     },
     setResults:function(results){
           this.weather= results;
     },
     dateBuilder(){
      let d= new Date();
      let months= ["January","February","March","April","May","June","July","August","September","October","November","December"];
      let days =["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];


      let day=days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year =d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
     }
     
 }
 
}
</script>

<style>
 * {
  margin:0px;
  padding: 0px;
  box-sizing:border-box;
 }
 body {
  font-family: 'montserrat',sans-serif;
 }
 #app {
  background-image:url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: center;
  transition: 0.4s;
   
 }
 
 #app.warm{
  background-image: url('./assets/warm-bg.jpg');
 }
 main {
  padding:25px;
  min-height: 100vh;
  background-image: linear-gradient(to bottom,rgba(0,0,0,0.25),rgba(0,0,0,0.75));
 }
 .search-box {
      width:100%;
      margin-bottom: 30px;
 }
 .search-box .search-bar {
  width: 100%;
  display: block;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance:none;
  border:none;
  background:none;
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);

 }
 .search-box .search-bar:focus{
  background-color: rgba(255,255,255,0.75);
  border-radius: 16px 0px 16px 0px;
 }
 .location-box .location {
  font-size: 32px;
  color: #FFF;
  text-align: center;
  font-weight: 500;
  text-shadow: 1px 2px 3px rgba(0,0,0,0.25);
 }
 .location-box .date {
  font-size: 20px;
  color: #FFF;
  font-style: italic;
  text-align: center;
  font-weight: 500;
 }
 .weather-box{
  text-align: center;

 }
 .weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color:#FFF;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color:rgba(255,255,255,0.25);
  margin:30px 0px;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
  border-radius: 16px;
 }
 .weather-box .weather {
    color: #FFF;
    font-size: 48px;
    font-weight: 700;
    font-style: italic;
     text-shadow: 3px 6px rgba(0,0,0,0.25);
 }
 .weather-box .pressure {
  color: #FFF;
    font-size: 25px;
    font-weight: 500;
    margin:10px auto;
    font-style: italic;
    text-shadow: 1px 2px rgba(0,0,0,0.25);
     box-shadow: 1px 2px rgba(0,0,0,0.25);
     display: inline-block;
    border-radius: 10px;

 }
 .weather-box .humidity {
  color: #FFF;
    font-size: 25px;
    font-weight: 600;
    margin:10px auto;
    font-style: italic;
    
     box-shadow: 1px 2px rgba(0,0,0,0.25);
     display: inline-block;
    border-radius: 10px;
    font-family: 'Ubuntu',sans-serif;

 }
 
</style>
