<template>
  <div class="home">
    <ion-item class="input">
      <ion-label position="floating">Ville</ion-label>
      <ion-input :value="search" @input="search = $event.target.value"></ion-input>
    </ion-item>
    <ion-button @click="getWeather" expand="block">Rechercher</ion-button>
    <ion-card>
      <ion-card-header>
            {{name}}
      </ion-card-header>
      <ion-card-content>
        {{currentTemp}}
        {{minTemp}}
        {{maxTemp}}
        {{humidity}}
        {{country}}
        {{wind}}
      </ion-card-content>
    </ion-card>
  </div>
</template>

<script>

const openWeather = process.env.VUE_APP_MY_WEATHER_API_KEY

export default {
  name: 'home',
  data(){
    return{
      search : '',
      currentTemp :'',
      minTemp : '',
      maxTemp : '',
      humidity : '',
      country : '',
      wind : '',
      name : '',
    }
  },
  methods :{
    getWeather(){
          let url = 'http://api.openweathermap.org/data/2.5/weather?q=' + this.search + '&APPID=8a490ab10108f24ace622abd4b6bd56a&units=metric'
          this.$http.get(url).then(response => {
                    this.currentTemp = response.data.main.temp;
                    this.minTemp = response.data.main.temp_min;
                    this.maxTemp = response.data.main.temp_max;
                    this.humidity = response.data.main.humidity;
                    this.country = response.data.sys.country;
                    this.wind = response.data.wind.speed;
                    this.name = response.data.name;
                    console.log(response)
                  })
                  .catch(error =>{
                    console.log(error)
                  })
      },
    },
}
</script>
<style>
</style>

