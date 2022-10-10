<template>
  <form @submit.prevent="addTechno">
    <label for="techno">Techno à ajouter</label>
    <br>
    <input type="text" name="techno" v-model="techToLearn">
    <br>
    <button type="submit">Ajouter</button>
  </form>
</template>

<script>
import { ref } from 'vue';
export default {
  setup(props, ctx) {
    let techToLearn = ref('');
    const addTechno = () => {
      console.log("Form | addTechno() | techToLearn.value ", techToLearn.value);
      ctx.emit("add", techToLearn.value);
      techToLearn.value = '';
    }
    return {
      techToLearn,
      addTechno,
    };
  }
}
</script>

<style>
button{
  background-color: orange;
  border-radius: 5px;
  padding: 5px;
  margin: 5px;
  border: 1px solid white;
}
button:hover{
  background-color: orangered;
}
input{
  border-radius: 5px;
  margin: 5px;
}
</style>