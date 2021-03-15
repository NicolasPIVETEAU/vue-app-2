<template>
  <div class="containerVille" v-if="result">
    <div class="infoBase">
      <h4>Qualité de l'air pour : <br>{{result.city.name}}</h4>
      <div class="panel">
        <h1>{{result.aqi}}</h1>
        <h3></h3>
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
        <td data-th="Movie Title">{{ particle }}</td>
        <td data-th="Genre">{{ value.v }}</td>
      </tr>
    </table>

  </div>
</template>

<script>
export default {
name: "displayDetails",
  props: {
    result: Object,
  }
}
</script>

<style scoped>

.infoBase{
  display: flex;
  flex-direction: column;
}
.panel{
  border-radius: 10px;
  border: 1px solid black;
  padding-bottom: 2vh;
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
