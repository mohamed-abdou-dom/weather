<template>
  <div id="app">
    <div class="main">
      <div class="overlay">
        <div class="search-box">
          <input type="text" v-model="query" class="search" placeholder="search your country" @keypress.enter="fetchWeather">
        </div>
        <div class="details text-center" v-if="typeof weather.main != 'undefined'">
          <div class="country">
            <h3>{{weather.name}}, {{weather.sys.country}}</h3>
          </div>
          <div class="degree">
            <span>{{weather.main.temp_max}}&deg;c Max</span>
          </div><br>
          <div class="degree">
            <span>{{weather.main.temp_min}}&deg;c Min</span>
          </div>
          <div class="country">
            <h3>{{weather.weather[0].main}}</h3>
          </div>
        </div>
        <div v-if="weather.cod == 404">
          <div class="details text-center">
            <div class="country">
              <h3>mak sure from country name</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      api_key: '9dc056e9b272ad94b847060bc935a6cc',
      url_base: 'https://api.openweathermap.org/data/2.5/weather',
      query: '',
      weather: {}
    }
  },
  methods:{
    fetchWeather(){
      if(this.query != ''){
        fetch(`${this.url_base}?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);
      }else{
        console.log('enter any thing');
      }
    },
    setResults(results){
      this.weather = results;
    }
  }
}
</script>

<style>

*{
  margin: 0;
  padding: 0;
}

.text-center{
  text-align: center;
}

::placeholder {
  color: #d5dcea;
}

.main{
  position: relative;
  height: 100vh;
  background-image: url('./assets/snow.jpg');
  background-size: cover;
  background-position: center;
}

.overlay{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
}

.search-box{
  width: 50%;
  margin: auto;
}

.search{
  width: 100%;
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.4);
  margin: 50px 0;
  border: none;
  border-radius: 0 16px;
  box-shadow: none;
  color: #d5dcea;
  font-size: 18px;
}

.search:focus{
  background-color: rgba(0, 0, 0, 0.2);
  border: none;
  border-radius: 16px 0;
  outline: none !important;
}

.details .country{
  color: #d5dcea;
  font-size: 30px;
  margin: 20px 0;
  text-transform: capitalize;
}

.details .degree{
  border: none;
  width: 50%;
  margin: auto;
  padding: 50px 40px;
  color: #ffffff;
  font-size: 60px;
  font-weight: 900;
  background-color: rgba(130, 123, 148, 0.5);
  border-radius: 5px;
}

</style>
