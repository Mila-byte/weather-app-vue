<template>
<div id="info">
  <p>Введите город:</p>
  <input type="text" v-model="city" @keydown.enter="getData">
  <input type="button" value="Искать" @click="getData">
  <p >Температура: {{ temp }} &#8451;</p>
  <p >Давление: {{ pressure }} hPa</p>
  <p >Скорость ветра: {{ windSpeed }} meter/sec</p>
</div>
</template>

<script>
export default {
  name: "InfoWindow",
  data () {
    return {
      city: '',
      temp: '0',
      pressure: '0',
      windSpeed: '0'
    }
  },
  methods: {
    async getData () {
        await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=fdc5c7b31d822cd909a6ffa9fab71737`)
            .then(res=>res.json())
            .then(res=> {
              if (res.cod >= 400 && res.cod < 500) {
                this.city = res.message
              } else if (res.cod === 200) {
                this.temp = +res.main.temp.toFixed()
                this.pressure = res.main.pressure
                this.windSpeed = res.wind.speed
                this.$emit('getLocation', res.coord)
              }
              console.log(res)
            })
            .catch(err => console.log(err))
    }
  }
}
</script>

<style scoped lang="scss">
#info {
  padding: 15px;
  p{
    margin: 15px 0;
  }
  input {
    &[type="text"] {
      min-width: 200px;
    padding: 10px;
      margin-top: 5px;
    }
    &[type="button"] {
      margin-top: 15px;
      cursor: pointer;
      padding: 10px;
    }
  }
}
</style>
