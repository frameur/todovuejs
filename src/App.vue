<template>
  <h1>&#8216;todo list&#8217;</h1>
  <Form @add="saveTechno" />

  <TechnoList :technos="technos" @delete-techno="deleteTechno" @edit-techno="editTechno" />
</template>

<script>

import Form from "@/components/Form";
import TechnoList from "@/components/TechnoList"
import { ref } from 'vue';
export default {
  name: 'App',
  components: {
    Form,
    TechnoList
    
  },
  setup(){
    let technos = ref([]);
    const saveTechno = function(data) {
      console.log("App | saveTechno() | data", data);
      technos.value = [...technos.value, {techno: data, id: Date.now() }];
       console.log("App | saveTechno() | technos.value", technos.value);
    };

    const editTechno = function(tech){
      technos.value = technos.value.map(t => t.id !== tech.id ? t : tech);
    }
    const deleteTechno = function (tech){
      console.log("App | deleteTechno() | tech", tech);
      technos.value = technos.value.filter(t => t.id !== tech.id )
    }
    return{
      saveTechno,
      deleteTechno,
      technos,
      editTechno,
    }
  }
}
</script>

<style>
body{
  background: black;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  

}

h1{
  
  text-transform: uppercase;
  text-shadow: 4px 4px 2px rgba(251, 247, 247, 0.6);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e1e5e9;
  margin-top: 60px;
}

</style>
