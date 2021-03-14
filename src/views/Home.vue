<template>
  <div class="home">

    <h2 style="padding: 0">Qualité de l'air dans le monde !</h2>
    <BaseMap />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/DetailsCountry.vue'
import BaseMap from '@/components/BaseMap.vue'

export default {
  name: 'Home',
  components: {
    BaseMap
  },
  data() {
    return {
      form: {
        pays: ''
      }
    }
  },
  methods: {
    submitForm() {

    }
  }
}
</script>
