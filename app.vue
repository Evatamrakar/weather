<template>
  <div class="container text-center py-5" >
    <div>
      <div class="mb-3">
        <div class="form-group">
        <label for="" class="px-2" >Cities</label>
        <select class="custom-select" name="" id="" v-model="name" @change="getUrl(name)" >
          <option selected>Select one</option>
          <option :value="city.name" v-for="(city,index) in cities.data.data" :key="index">{{ city.name }}</option>
        </select>
      </div>
      </div>
    </div>
    <h1>{{ weather.weather[0].main }}</h1>
    <div>
      <img src="~assets/rain.gif" alt="" v-if="weather.weather[0].main == 'Rain'">
    </div>
    <div>
      <img src="~assets/cloudy.gif" alt="" v-if="weather.weather[0].main == 'Clouds'">
    </div>
   
    <div>{{weather.weather[0].description}}</div>
    <h1>{{ weather.main.temp }}°C</h1>
    <div>Feels like {{ weather.main.feels_like}}°C</div>

    <h1>Wind speed {{ weather.wind.speed }} km/hr</h1>
  </div>
</template>

<script setup>
const name = "Dharan"
const url = ref(`https://api.openweathermap.org/data/2.5/weather?q=Dharan&appid=6e8ca986d16e44aabcb577c1868fe659&units=metric`);

const {data:cities} = await useFetch("https://www.nepallocation.com.np/api/v1/city/list", {headers: {'Authorization' :"Bearer T3vIFM2-kg5Ky-I20MeuWLr9"}});

const {data, pending} = useFetch(url, { refetch: true});
function getUrl(weather) {
  url.value =`https://api.openweathermap.org/data/2.5/weather?q=${cities}&appid=6e8ca986d16e44aabcb577c1868fe659&units=metric`;
}
</script>

<style scoped>

</style>