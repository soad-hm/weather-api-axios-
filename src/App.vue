
<script>
import axios from'axios'
export default {
  name:'App',
  data(){
    return{
      api_key:'994600024dfa6ee2da0f8205ba3dcd51',
      api:'https://api.openweathermap.org/data/2.5/',
      query:"",
      Weather:{}
    }
  },
  methods:{
    fetchweather(e){
   if(e.key =='Enter'){
    // fetch(`${this.api}weather?q=${this.query}&appid=${this.api_key}`)
    // .then(res=>{return res.json()})
    // .then(respons=>{console.log(respons),this.Weather=respons})
    // .then()
    axios.get(`${this.api}weather?q=${this.query}&appid=${this.api_key}`)
    .then(respons=>{this.Weather=respons.data})
    }
    },
    information(){
      let months=["January","February","March","April","May","June","July","August","September","October","November","December"]
      let days=["sant","sun","mon","tue","wen","thr","fri" ]
      let d=new Date()
      let day=days[(d.getDay())+1]
      let date=d.getDate()
      let month=months[(d.getMonth())]
      let year=d.getFullYear()
      return`${day} ${date} ${month} ${year}`
    }
  }
 }
</script>

<template>
<div id="App">
  <main>
     <div class="SearchBox">
       <input
       type="text"
       placeholder="Search"
       class="Search-Bar"
       v-model="query"
       @keypress="fetchweather">
     </div>
     <div v-if="(typeof Weather.main!='undefined')">
     <div class="Location-Box">
      <div class="Location">{{Weather.name}},{{ Weather.sys.country }}</div>
      <div class="Date">{{information()}}</div>
      </div>
      <div class="WeatherApp">
        <div class="Temp"> {{(Math.floor(Weather.main.temp))-271}} C</div>
        <div class="Weather"> {{Weather.weather[0].main}}</div>
      </div>

     </div>
     <div class="background-container">
     <img src="./img/wolfgang-hasselmann-bR_-gllg7Bs-unsplash.jpg" alt="Background Image" class="background-image">
     </div>
 
  </main>
</div> 

</template>
<style scoped>
.background-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  filter: blur(3px); 
  z-index: -1; 
}

.background-image {
  object-fit: cover;
  width: 100%;
  height: 100%;
  pointer-events: none; }
.Search-Bar{
  width: 50rem;
  height: 2rem;
  margin: auto;
  display: flex;
  align-content: center;
  justify-content: center;
  margin-top: 2.5rem;
  border:0.2rem solid rgb(99, 99, 137);
  border-bottom-right-radius: 1rem;
  border-top-left-radius: 1rem;
  background-color: rgb(124, 121, 117);
  color: rgb(255, 255, 255);
  font-size: large;
}
input:focus {
  outline: none;
}
.Location{
  color: white;
  font-size: 3rem;
  margin: auto;
  display: flex;
  align-content: center;
  justify-content: center;
  margin-top: 4rem;
}
.Date{
  color: white;
  font-size: 1.5rem;
  margin: auto;
  display: flex;
  align-content: center;
  justify-content: center;
}
.Temp{
  width: 15rem;
  height: 7.5rem;
  background-color: rgb(124, 121, 117);
  margin: auto;
  display: flex;
  align-content: center;
  justify-content: center;
  margin-top: 2rem;
  border-radius: 3rem;
  color: aliceblue;
  font-size: xx-large;
  padding-top: 5rem;

}
.Weather{
  font-size: 3rem;
  margin: auto;
  display: flex;
  align-content: center;
  justify-content: center;
  margin-top: 2.5rem;
}



</style>