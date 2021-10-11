<template>
  <div>
      <h3>#{{num}} {{pokeName}}</h3>
      <h4 v-for="(type, index) in types" :key="index">{{type}}</h4>
      <img :src="frontImage">
  </div>
</template>

<script>
import axios from "axios";

export default {
    props:{
        name: String,
        url: String,
        num: Number
    },
    created: function(){
        axios.get(this.url).then(res =>{
            this.frontImage = res.data.sprites.front_default;
            this.backImage = res.data.sprites.back_default;
            res.data.types.forEach(item =>{
                this.types.push(item.type.name)
            })


        })
    },
    data(){
        return {
            frontImage:"",
            backImage:"",
            types:[]
        }
    },
    computed:{
        pokeName(){
            return this.name.charAt(0).toUpperCase() + this.name.slice(1);
        }
    }
}
</script>

<style>

</style>