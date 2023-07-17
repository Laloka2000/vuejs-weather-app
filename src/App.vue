
<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 
    ? 'warm' : ''">
    <main>
      <div class="city-search">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather"
        >
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ currentDate() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp)}}˚C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>




<script>
export default {
  name: 'app',
  data(){
    return {
      api_key:'e9aedb5a5abb1d486dfbbd72bc3dbd75',  //változók jöhetnek ide
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e){
      if(e.key =="Enter"){
        //api hívása 
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res => {
              return res.json();
            }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    },
    currentDate(){
      let c = new Date();
      // Más megoldás moment js
      
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ];

      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thrusday",
        "Friday",
        "Saturday"
      ];

      let day = days[c.getDay()];
      let date = c.getDate();
      let month = months[c.getMonth()];
      let year = c.getFullYear();

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
  font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

}


#app{
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4;
}


#app.warm{
  background-image: url('./assets/warm-bg.jpg');
}


main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}


.city-search{
  width: 100%;
  margin-bottom: 30px;
}


.city-search .search-bar{
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 20px 0px 20px;
  transition: 0.4;
}

.city-search .search-bar{
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.75);
  border-radius: 20px 0px 20px 0px;
}


.location-box .location{
  color: #fff;
  font-size: 32px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}


.location-box .date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}


.weather-box{
  text-align: center;
}


.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 20px;
  margin: 30px 0px;

  box-shadow: 10px 10px rgba(0,0,0,0.25);
}



.weather-box .weather{
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
}

</style>
