<template>
  <section>
  <div class="home">
    <ion-item class="input">
      <ion-label class="label">Ville</ion-label>
      <ion-input :value="search" @input="search = $event.target.value"></ion-input>
    </ion-item>
    <ion-button @click="getWeather" expand="block">Rechercher</ion-button>
    <ion-card>
      <ion-card-header>
            {{name}}
      </ion-card-header>
      <ion-card-content>
        {{myDate}}
        {{currentTemp}}
        {{minTemp}}
        {{maxTemp}}
        {{humidity}}
        {{country}}
        {{wind}}
        {{description}}
        <img v-bind:src="icon" style="width: 20%;">
      </ion-card-content>
    </ion-card>
  </div>
  </section>
</template>

<script>

const openWeather = process.env.VUE_APP_MY_WEATHER_API_KEY

export default {
  name: 'home',
  data(){
    return{
      search : '',
      myDate : new Date().toISOString().slice(0, 10),
      currentTemp :'',
      icon:'',
      minTemp : '',
      maxTemp : '',
      humidity : '',
      country : '',
      wind : '',
      name : '',
      description : '',
    }
  },
  methods :{
    getWeather(){
          let url = 'https://api.openweathermap.org/data/2.5/weather?q=' + this.search + '&APPID=8a490ab10108f24ace622abd4b6bd56a&units=metric&lang=fr'
          this.$http.get(url).then(response => {
                    this.currentTemp = response.data.main.temp.toFixed(0);
                    this.minTemp = response.data.main.temp_min.toFixed(0);
                    this.maxTemp = response.data.main.temp_max.toFixed(0);
                    this.humidity = response.data.main.humidity;
                    this.country = response.data.sys.country;
                    this.wind = response.data.wind.speed;
                    this.name = response.data.name;
                    this.description = response.data.weather[0].description;
                    this.icon = "http://openweathermap.org/img/w/"+response.data.weather[0].icon + '.png';
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
  .home{
    width:100%;
    display: flex;
    flex-direction: column;
  }
  section{
    width: 100%;
    display: flex;
    background-color: black;
  }
  .input{
    width: 100%;
    background-color: red;
    margin: 0;
  }

</style>

