<template>
  <div>
    <form v-on:submit.prevent="submitForm" method="post">
      <div class="form-group">
        <input type="text" class="form-control" id="name" placeholder="Choisissez une Ville" v-model="posts.ville">
        <button class="btn btn-primary">Submit</button>
      </div>
    </form>

   <DisplayDetails :result="result" />

  </div>

</template>


<script>

import axios from 'axios';
import displayDetails from "@/components/displayDetails";
import DisplayDetails from "@/components/displayDetails";

export default {
  name: 'details',
  components: {DisplayDetails},
  data(){
    return{
      posts: {
        ville:null
      },
      result:undefined
    }
  },
  created(){
    this.posts.ville = this.$route.query.villeInfo
    this.submitForm(null)
  },
  methods:{
    async submitForm(e){
      console.log(this.posts.ville)
      let ville = this.posts.ville.replaceAll(' ','-').toLowerCase()
      console.log(ville)
      let data = []
      const response = await axios.get(`https://api.waqi.info/feed/${ville}/?token=ad62ba964a0eb5292ce0f5cc1c3ed90873b0d757`)
                                  .then(response => data = response.data.data)
                                  .catch(error => console.log(error))

      console.log(data)
      this.result = data;

    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.containerVille{
  margin: auto;
  margin-top: 5vh;
  padding: 10px;
  display: flex;
  flex-direction: column;
  border-radius: 10px;
  box-shadow: 5px 5px 10px grey;
  width: 30%;
}
</style>
