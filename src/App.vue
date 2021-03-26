<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld v-for="(todo, index) in todos" :key="index" :todo="todo" />

    <div v-on:click="showText">{{ active }}</div>
    <input v-if="text" v-model="active" />
    <div v-else>{{ textReverse }}</div>
    <div v-bind:class="bind">
      {{ text ? "bind" : "feter" }}
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      todos: [
        { id: 1, name: "Tim", lastName: "Borisyuk" },
        { id: 2, name: "123", lastName: "Borisyuk" },
        { id: 3, name: "321", lastName: "Borisyuk" },
      ],
      active: "abcd",
      bind: "bind",
      text: true,
    };
  },
  methods: {
    showText() {
      this.text = !this.text;
    },
  },
  computed: {
    textReverse() {
      return this.active
        .split("")
        .reverse()
        .join("");
    },
  },
  watch: {
    text() {
      console.log("text изменился");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  max-width: 1000px;
  height: 600px;
}
img {
  /* display: block; */
  max-width: 100%;
}
.bind {
  color: red;
}
.feter {
  color: green;
}
</style>
