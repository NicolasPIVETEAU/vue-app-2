<template>
  <div class="details">
    <h1>Détails de la pollution</h1>
      <DetailsCountry/>
    </div>
</template>


<script>
import DetailsCountry from '@/components/DetailsCountry.vue'
import BaseMap from "@/components/BaseMap";

export default {
  name: "details",
  components: {
    DetailsCountry
  }
};
</script>
