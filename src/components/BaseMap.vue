<template>
  <div id="mapContainer" class="basemap">
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";
import 'mapbox-gl/dist/mapbox-gl.css';
import axios from 'axios';




export default {

  name: "BaseMap",
  data() {
    return {
      accessToken: 'pk.eyJ1IjoiemVzcG9uZ2Vib2IiLCJhIjoiY2ttM2N1OWxuM2ZldDJwcDNnaDh4dzk2YiJ9.ju6b_0a6hrtytFtjqN1f_A',
    };
  },

  async mounted() {

    mapboxgl.accessToken = this.accessToken;

    const countries = ["Paris", "london", "inde", "rome","berlin", "calgary", "moscow", "madrid", "Salvador", "brasilia",
       "bern", "ankara", "iran", "varsovie", "pekin", "sidney", "bangkok"]


    const map = new mapboxgl.Map({
      container: "mapContainer",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [46.232193, 2.209667],
      zoom: 1,
    });

    const nav = new mapboxgl.NavigationControl();
    map.addControl(nav, "top-right");

    const geolocate = new mapboxgl.GeolocateControl({
      positionOptions: {
        enableHighAccuracy: true
      },
      trackUserLocation: true
    });

    map.addControl(geolocate, "top-right")

    for (const country of countries) {
      let data = [];

      await axios.get(`https://api.waqi.info/feed/${country}/?token=ad62ba964a0eb5292ce0f5cc1c3ed90873b0d757`, {
        method: 'GET',
        mode: 'no-cors'
      }).then(response => data = response.data.data)

      console.log(data.aqi)

      let coloration = ""
      let colorationTitle = ""
      let description =""
      if(data.aqi < 50){
        coloration = "#009966"
        colorationTitle = "white"
        description = "Good"
      }if(data.aqi > 50 && data.aqi < 100){
        coloration = "#ffde33"
        colorationTitle = "black"
        description = "Moderé"
      }if(data.aqi > 100 && data.aqi < 150){
        coloration = "#ff9933"
        colorationTitle = "black"
        description = "Malsain"
      }if(data.aqi > 150){
        coloration = "#cc0033"
        colorationTitle = "white"
        description = "Danger"
      }

      var test = 'paris';

      var popup = new mapboxgl.Popup({closeOnClick: false})
          .setLngLat(data.city.geo.reverse())
          .setHTML(`<a href="/#/details?villeInfo=${country}" style="text-decoration: none"><div style='padding: 3px; background-color: ${coloration};color: ${colorationTitle};max-width:100px; min-width: 50px;text-align:center;'><small>${country.toUpperCase()}</small> <div style='font-size:15px;height:20px;padding-top:2px;'>${data.aqi}</div>${description}</div></a>`)
          //.setHTML(`<a @click="testRouter" style="text-decoration: none"><div style='padding: 3px; background-color: ${coloration};color: ${colorationTitle};max-width:100px; min-width: 50px;text-align:center;'><small>${country.toUpperCase()}</small> <div style='font-size:15px;height:20px;padding-top:2px;'>${data.aqi}</div>${description}</div></a>`)
          .addTo(map);
    }
  },
  methods: {

  }
};


</script>

<style scoped>
.basemap {
  width: 100%;
  height: 85vh;
}
</style>

