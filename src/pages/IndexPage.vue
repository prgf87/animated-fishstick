<template>
  <q-page padding>
    <input v-model="message" @keyup="handleKeyUp"/>
    <button @click="clearMessage" >Clear Text</button>
    <h5>{{ message }}</h5>
  </q-page>
</template>

<script lang="ts">
  export default {
    data(){
       return {
         message: "I am VueJS!"
       }
    },
    methods:{
      clearMessage(){
        this.message = ''
      },
      handleKeyUp(event){
        console.log(event)
      }
    }
  }
</script>
