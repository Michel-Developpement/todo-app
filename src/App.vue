<template>
  <h1>Veille techno</h1>
  <FormTechno @add="saveTechno" />
  <br />
  <TechnoList :technos="technos" @delete-techno="deleteTechno" @edit-techno="editTechno" />
</template>

<script>
import FormTechno from "@/components/FormTechno";
import TechnoList from "@/components/TechnoList"
import { ref } from "@vue/reactivity";
export default {
  name: "App",
  components: {
    FormTechno,
    TechnoList
  },
  setup() {
    let technos = ref([]);
    const saveTechno = (data) => {
      console.log("App | saveTechno() | data ", data);
      technos.value = [...technos.value, { techno: data, id: Date.now() }];
      console.log("App | saveTechno() | technos.value ", technos.value);
    };
    const editTechno = (tech) =>{
      technos.value = technos.value.map(t => t.id != tech.id ? t : tech);
    }
    const deleteTechno = (tech) =>{
      console.log("App | deleteTechno() | tech", tech)
      technos.value = technos.value.filter(t => t.id !== tech.id);
    }
    return { saveTechno, deleteTechno, editTechno, technos };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #3b3b3b;
  color: #f3f3f3;
  margin-top: 60px;
  padding: 15px 0;
}
body{
  background-color: #3b3b3b;
}
</style>
