<template>
  <div class="containerVille" v-if="result">
    <div class="infoBase">
      <h4>Qualité de l'air pour : <br>{{result.city.name}}</h4>
      <div :class="{'good': result.aqi < 50, 'medium': result.aqi > 50 && result.aqi < 100, 'hard': result.aqi > 100 && result.aqi < 150, 'danger': result.aqi > 150}">
        <h1>{{result.aqi}}</h1>
        <h3>{{ description(result.aqi) }}</h3>
      </div>
    </div>
    <div class="specific">
      <p>{{result.time.s}}</p>
    </div>

    <table>
      <tr>
        <th>Particules</th>
        <th>Taux (µg/m3)</th>
      </tr>
      <tr v-for="(value, particle) in result.iaqi">
        <td result-th="Movie Title">{{ particle }}</td>
        <td result-th="Genre">{{ value.v }}</td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
  name: "displayDetails",
  props: {
    result: Object,
  },
  methods: {
    description(aqi) {
      console.log("----" + aqi)
      if (aqi < 50) {
        return "Good"
      }
      if (aqi > 50 && aqi < 100) {
        return "Modéré"
      }
      if (aqi > 100 && aqi < 150) {
        return "Malsain"
      }
      else{
        return "Danger"
      }
    }
  }
}
</script>

<style scoped>

.infoBase{
  display: flex;
  flex-direction: column;
}
.good{
  border-radius: 10px;
  padding-bottom: 2vh;
  background-color: #009966;
  color: white;
}
.medium{
  border-radius: 10px;
  padding-bottom: 2vh;
  background-color: #ffde33;
}
.hard{
  border-radius: 10px;
  padding-bottom: 2vh;
  background-color: #ff9933;
}
.danger{
  border-radius: 10px;
  padding-bottom: 2vh;
  background-color: #cc0033;
  color: white;

}
table {
  border: 1px solid #ccc;
  border-collapse: collapse;
  margin: 0;
  padding: 0;
  width: 100%;
  table-layout: fixed;
  border-radius: 10px;
}

table caption {
  font-size: 1.5em;
  margin: .5em 0 .75em;
}

table tr {
  background-color: #f8f8f8;
  border: 1px solid #ddd;
  padding: .35em;
}

table th,
table td {
  padding: .625em;
  text-align: center;
}

table th {
  font-size: .85em;
  letter-spacing: .1em;
  text-transform: uppercase;
}

</style>
