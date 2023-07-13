<template>
  <div class="container text-center py-5" >
    <div>
      <div class="mb-3">
        <div class="form-group">
        <label for="" class="px-2">City</label>
        <select class="custom-select" name="" id="" v-model="name" @change="getUrl(name)" >
          <option selected>Select one</option>
          <option :value="city.name" v-for="(city,index) in cities.data.data" :key="index">{{ city.name }}</option>
        </select>
      </div>
    </div>
    </div>
    <section v-if="pending" >
     <img src="~assets/Loading.gif" alt="">
    </section>

    <section class="container m-auto" v-else>
      <h1>City: {{weather.name }}</h1>
      <h1>{{ weather.weather[0].main }}</h1>
      <div>
        <img src="~assets/rain.gif" alt="" v-if="weather.weather[0].main == 'Rain'">
      </div>
      <div>
       <img src="~assets/cloudy.gif" alt="" v-if="weather.weather[0].main == 'Clouds'">
      </div>
      <div>
       <img src="~assets/sunny.gif" alt="" v-if="weather.weather[0].main == 'Sunny'">
      </div>
      <div>
       <img src="~assets/windy.gif" alt="" v-if="weather.weather[0].main == 'Windy'">
      </div>
   
      <div>
        {{weather.weather[0].description}}
      </div>
      <h1>{{ weather.main.temp }}°C</h1>
      <div>
        Feels like {{ weather.main.feels_like}}°C
      </div>

      <h1>Wind speed {{ weather.wind.speed }} km/hr</h1>
    </section>
  </div>
</template>

<script setup>
let name = ref("Dharan")
const url = ref(
  `https://api.openweathermap.org/data/2.5/weather?q=Dharan&appid=6e8ca986d16e44aabcb577c1868fe659&units=metric`
  );

const {data: cities} = await useFetch("https://www.nepallocation.com.np/api/v1/city/list", {headers: {'Authorization' :"Bearer T3vIFM2-kg5Ky-I20MeuWLr9"}});

const {data:weather, pending} = await useFetch(url, {refetch: true});
function getUrl(city) {
  url.value =`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=6e8ca986d16e44aabcb577c1868fe659&units=metric`;
};
</script>

<style scoped>

</style>