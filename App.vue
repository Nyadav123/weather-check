<template>
<div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp> 16 ? 'warm' :''  && weather.main.temp< 16 ? 'cold' :''">

<main>
<div class="search-box">
<input 
 type="text" 
 class="search-bar" 
 placeholder="search....."
 v-model="query"
 @keypress="fetchWeather" />

 </div>
   <div class="weather-wrap" v-if="typeof weather.main != 'undefined' "> 
   <div class="location-box"> 
   <div class="location"> {{ weather.name }} , {{weather.sys.country}} </div>
   <div class="date"> {{dateBuilder()}}</div>
   </div>
   <div class="weather-box">
   <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
   <div class="weather">{{ weather.weather[0].main}}</div>
   </div>
   </div>
   
   
</main>
</div>
</template>

<script>


export default {
  name: 'App',
  data(){
    return {
      api_key: '90a9789303583761bf16e4f2bd29d299',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
    methods: {
      fetchWeather(e) {
        if (e.key == "Enter") {
             fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
             .then(res => {
               return res.json();
             }).then(this.setResults);
        }
      },
      setResults (results) {
        this.weather = results;
      },
       dateBuilder () {
      let d = new Date();
      let months = ["January","february","March","April","may","june","july","august","september","october","november","december"];
      let days = ["SUNDAY","MONDAY","TUESDAY","WEDNESDAY","THURSDAY","FRIDAY","SATURDAY"];

let day = days[d.getDay()];
let date = d.getDate();
let month = months[d.getMonth()];
let year = d.getFullYear();

return `${day} ${date} ${month} ${year}`;
    }

    }
 
  
}
</script>

<style>
*{
margin: 0;
padding: 0;
box-sizing: border-box;

}
body{
font-family: cursive;

}
#app{
    background-image: url('https://source.unsplash.com/weekly?https://www.google.com/imgres?imgurl=https%3A%2F%2Fimages.theconversation.com%2Ffiles%2F232705%2Foriginal%2Ffile-20180820-30593-1nxanpj.jpg%3Fixlib%3Drb-1.1.0%26q%3D45%26auto%3Dformat%26w%3D496%26fit%3Dclip&imgrefurl=https%3A%2F%2Ftheconversation.com%2Fwhy-the-weather-forecast-will-always-be-a-bit-wrong-101547&tbnid=w_O3LH5-uXWy1M&vet=12ahUKEwi48b269pnxAhXLh_0HHVm1CGMQMygCegUIARDTAQ..i&docid=LUjGDfBrhkmcZM&w=496&h=331&q=weather%20images&ved=2ahUKEwi48b269pnxAhXLh_0HHVm1CGMQMygCegUIARDTAQ');
    
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  #app.warm{
    background-image:url('https://source.unsplash.com/user/erondu/daily')

  }
  #app.cold{
    background-image:url('https://source.unsplash.com/user/jackie/likes/1600x900')

  }
main{
min-height: 100vh;
padding: 25px;
background-image:linear-gradient( to bottom , rgba(0,0,0,0.75));}
.search-box{
width: 100%;
margin: 5px;
}
.search-box .search-bar{
display: block;
width: 100%;
padding: 15px;
color: #313131;
font-size:20px;
appearance: none;
border: none;
outline: none;
box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
background-color: rgba(255,255,255,0.55);

border-radius: 0px 16px 0px 16px;
transition: 0.4s;}

.search-box .search-bar:focus {
box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
background-color: rgba(255,255,255,0.75);
border-radius:16px 0px 16px 0px;
}
 .location-box .location {
 color: #fff;
 font-size: 32px;
 font-weight:500 ;
 text-align: center;
 text-shadow: 1px 3px rgba(0,0,0,0.25);
 }
 .location-box .date {
 color: #fff;
 font-size: 20px;
 font-weight: 300;
 font-style: italic;
 text-align: center;
 }
 .weather-box {
 text-align: center;}

 .weather-box .temp {
 display:inline-block;
 padding:10px 25px;
 color: #FFF;
 font-size: 102px;
 font-weight: 900;
 text-shadow:3px 6px rgba(159, 151, 151, 0.25);
 background-color: rgba(255,255,255,0.25);
 border-radius: 16px;
 margin:30px 0px;
 box-shadow: 3px 6px rgba(0,0,0,0.25);

 }
 .weather-box .weather{
 color:#FFF;
 font-size: 48px;
 font-style:italic;
 font-weight: 700;
 text-shadow: 3px 6px rgba(0,0,0,0.25);

 
 }



</style>
