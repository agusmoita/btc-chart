<template>
  <div id="app">
    <grafico :chartData="datos" :height="100" :width="200"></grafico>
  </div>
</template>

<script>

import moment from 'moment'
import Grafico from './components/Grafico.vue'

const colores = {
  amarillo: 'rgba(255, 206, 86)',
  azul: 'rgba(54, 162, 235)'
}

export default {
  name: 'App',
  data () {
    return {
      datos: null
    }
  },
  components: {
    Grafico
  },
  mounted () {
    const MINUTOS = 10
    this.obtener()
    setInterval(this.obtener, MINUTOS * 60 * 1000)
  },
  methods: {
    async obtener () {
      const response = await fetch('https://api.coindesk.com/v1/bpi/historical/close.json')
      const data = await response.json()
      const bpi = data.bpi
      this.datos = {
        labels: Object.keys(bpi).map(k => moment(k).format('DD-MM')),
        datasets: [
          {
            label: 'Precio Bitcoin',
            backgroundColor: colores.amarillo,
            pointBackgroundColor: colores.amarillo,
            pointBorderColor: colores.azul,
            pointRadius: 4,
            borderColor: colores.azul,
            lineTension: 0.4,
            fill: false,
            data: Object.values(bpi).map(k => k)
          }
        ]
      }
    }
  }
}
</script>
