<template>
  {{ todos.length }} Achat{{ todos.length > 1 ? "s" : "" }}

  <h3>&#8216;ma liste de course&#8217;</h3>

  <ul>
    <li v-for="tod in todos" :key="tod.id">
      <button class="buttonModif" @click="editTodo(tod)">Modifier</button>
      <button class="buttonSuppr" @click="deleteTodo(tod)">
        Supprimer
      </button>
      <div class="resultList">
        <span v-if="todoToEdit !== null && todoToEdit.id === tod.id">
          <input
            class="inputSave"
            type="text"
            v-model="todoToEdit.todo"
            @keypress.enter="save"
          />

          <button class="buttonSave" @click="save">&#9996;</button>
        </span>
        <span v-else>
          {{ tod.todo }}
        </span>
      </div>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";
export default {
  emits: ["delete-todo", "edit-todo"],
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
  setup(props, { emit }) {
    let todoToEdit = ref(null);
    let deleteTodo = function(tod) {
      emit("delete-todo", tod);
    };
    let editTodo = function(tod) {
      todoToEdit.value = tod;
    };
    let save = function() {
      emit("edit-todo", todoToEdit.value);
      todoToEdit.value = null;
    };
    return {
      deleteTodo,
      editTodo,
      save,
      todoToEdit,
    };
  },
};
</script>

<style scoped>
h3 {
  text-transform: uppercase;
  color: #aade7c;
}
ul {
  display: grid;
  grid-auto-columns: 1fr;
}

span {
  position: relative;
  text-align: left;
  margin-top: 5%;
  margin-left: 50px;
  font-size: 20px;
  text-transform: uppercase;
  color: yellow;
  width: 300px;
}
ul li {
  display: flex;
  justify-content: center;
  width: 80%;
  margin-bottom: 10px;
  list-style: none;
}
button {
  margin: 5px;
}
div .resultList {
  display: flex;
  background: #065099;
  border: 2px solid yellow;
  border-radius: 5px;
  margin-left: 5px;
  font-weight: bold;
}

/* input sauvegarder */

.inputSave {
  padding: 5px;
  font-size: 13px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  border-width: 2px;
  border-color: #d61212;
  background-color: #ffffff;
  color: #1b0505;
  border-style: groove;
  border-radius: 6px;
  box-shadow: 0px 0px 12px rgba(66, 66, 66, 0.75);
  text-transform: uppercase;
}
.inputSave:focus {
  outline: none;
}

/* button sauvegarder */
.buttonSave {
  box-shadow: inset 0px 1px 0px 0px #caefab;
  background: linear-gradient(to bottom, #77d42a 5%, #5cb811 100%);
  background-color: #77d42a;
  font-size: 20px;
  font-weight: 800;
  border-radius: 50%;
  border: 1px solid #268a16;
  display: inline-block;
  cursor: pointer;
  color: #306108;
  font-family: Arial;
  text-decoration: none;
  text-shadow: 0px 1px 0px #aade7c;
  display: inline-block;
  position: absolute;
  margin: auto;
}
.buttonSave:hover {
  transform: scale(2);
  transition: 0.8s;
}

/* button modifier */
.buttonModif {
  box-shadow: 3px 4px 0px 0px #1564ad;
  background: linear-gradient(to bottom, #79bbff 5%, #127eeb 100%);
  background-color: #79bbff;
  border-radius: 5px;
  border: 1px solid #337bc4;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 15px;
  font-weight: bold;
  padding: 15px 44px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #528ecc;
}
.buttonModif:hover {
  background: linear-gradient(to bottom, #065099 5%, #79bbff 100%);
  background-color: #378de5;
}

/* button supprimer */
.buttonSuppr {
  box-shadow: 3px 4px 0px 0px #ab1616;
  background: linear-gradient(to bottom, #270101 5%, #a70715 100%);
  background-color: #f00927;
  border-radius: 5px;
  border: 1px solid #e0240b;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 15px;
  font-weight: bold;
  padding: 15px 44px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #c80b0b;
}
.buttonSuppr:hover {
  background: linear-gradient(to bottom, #3f0202 5%, #f5071b 100%);
  background-color: #e35b39;
}

input {
  margin-bottom: 2px;
}
@media screen and (max-width: 620px) {
  span {
    width: 150px;
    font-size: 12px;
    text-align: center;
    margin: auto;
  }
  .buttonModif,
  .buttonSuppr {
    width: 100px;
    font-size: 12px;
    text-align: left;
    margin-left: auto;
    padding: 10px;
  }
  .buttonSave {
    font-size: 12px;
  }
}
</style>
