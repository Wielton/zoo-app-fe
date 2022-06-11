<template>
  <div class="hello">
    <input 
    v-model="animalName"
    type="text" name="" id="nameInput">
    <input
    v-model="imageURL"
    type="text" name="" id="nameInput">
    <button @click="postAnimal">POST</button>
    <div>
      <button @click="getAnimals">GET</button>
      {{animalArr}}
    </div>
    
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data () {
    return {
      animalName: null,
      imageURL: null,
      animalArr : []
    }
  },
  methods: {
    postAnimal(){
      axios.request({
        url : "http://127.0.0.1:5000/api/animalsdb",
        method : "POST",
        data : {
          animalName : this.animalName,
          imageURL : this.imageURL
        }
    }).then((response)=>{
      console.log(response)
      }).catch((error)=>{
        console.log(error)
      })
    },
    getAnimals(){
      axios.request({
        url : "http://127.0.0.1:5000/api/animalsdb",
        method : "GET"
    }).then((response)=>{
      this.animalArr = response.data;
      console.log('This ran')
      }).catch((error)=>{
        console.log(error)
      })
    },
    
  },
  mounted(){
      this.getAnimals();
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
