<template>
  <form @submit.prevent="addTodo">
    <label for="todo"></label>
    <br />
    <input
      class="inputAdd"
      type="text"
      name="todo"
      v-model="todTobuy"
      required
    />
    <br />
    <button class="buttonAdd" type="submit">Ajouter</button>
  </form>
</template>

<script>
import { ref } from "vue";
export default {
  setup(props, ctx) {
    let todTobuy = ref("");

    const addTodo = function() {
      console.log("form | addTodo | todTobuy.value", todTobuy.value);
      ctx.emit("add", todTobuy.value);
      todTobuy.value = "";
    };

    return {
      todTobuy,
      addTodo,
    };
  },
};
</script>

<style scoped>
/* input ajouter */
.inputAdd {
  padding: 5px;
  font-size: 18px;
  border-width: 3px;
  border-color: #d61212;
  background-color: #ffffff;
  color: #1b0505;
  border-style: groove;
  border-radius: 6px;
  box-shadow: 0px 0px 12px rgba(66, 66, 66, 0.75);
  text-shadow: 4px 3px 4px rgba(218, 24, 90, 0.6);
  text-transform: uppercase;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
.inputAdd:focus {
  outline: none;
}

/* button ajouter */
.buttonAdd {
  box-shadow: inset 0px 1px 0px 0px #54a3f7;
  background: linear-gradient(to bottom, #007dc1 5%, #0061a7 100%);
  background-color: #007dc1;
  border-radius: 3px;
  border: 1px solid #124d77;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 13px;
  padding: 6px 24px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #154682;
}
.buttonAdd:hover {
  background: linear-gradient(to bottom, #0061a7 5%, #007dc1 100%);
  background-color: #0061a7;
}
</style>
