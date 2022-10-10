<template>
  <h3>Toutes les technos à veiller :</h3>
  {{ technos.length }} techno{{ technos.length > 1 ? "s" : "" }}
  <ul>
    <transition-group name="fade">
      <li v-for="tech in technos" :key="tech.id">
        <button @click="deleteTechno(tech)">Suppr</button>
        <button @click="editTechno(tech)">Edit</button>
        <span v-if="technoToEdit !== null && technoToEdit.id === tech.id">
          <input
            type="text"
            v-model="technoToEdit.techno"
            @keypress.enter="save"
          /><button @click="save">sauvegarder</button></span
        >
        <span v-else><p>{{ tech.techno }}</p></span>
      </li>
    </transition-group>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  emits: ["delete-techno", "edit-techno"],
  props: {
    technos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let technoToEdit = ref(null);
    let deleteTechno = (tech) => {
      emit("delete-techno", tech);
    };
    let editTechno = (tech) => {
      technoToEdit.value = tech;
    };
    let save = () => {
      emit("edit-techno", technoToEdit.value);
      technoToEdit.value = null;
    };
    return { deleteTechno, editTechno, technoToEdit, save };
  },
};
</script>

<style>
ul {
  list-style: none;
  width: 50%;
  margin-left: 100px;
  text-align: left;
}
li{
  background-color: rgb(137, 137, 137);
  border-radius: 5px;
  color: black;
  margin: 5px 0;
}
li:hover{
  background-color: rgb(45, 45, 45);
  color: white;
}
li span p {
  margin-left: 20px;
  display: inline;
}
.fade-enter-from {
  opacity: 0;
  transform: translateY(-200%);
}
.fade-enter-to {
  opacity: 1;
  transform: translateY(0%);
}
.fade-enter-active {
  transition: all 0.5s ease;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-to {
  opacity: 0;
}
.fade-leave-active {
  transition: all 1.3s ease;
}
/* .apear-enter-active,
.apear-leave-active {
  transition: opacity 0.5s ease;
}

.apear-enter-from,
.apear-leave-to {
  opacity: 0;
} */
</style>