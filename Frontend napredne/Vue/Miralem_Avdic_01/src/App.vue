<template>
  <div id="app" class="container">
    <h2>To Do</h2>
    <ul>
      <li
        v-for="(item, index) in items"
        :key="item.id"
        v-bind:style="{ 'text-decoration': item.done ? 'line-through' : 'none' }"
        v-on:click="toggleDone(index)"
      >
        <input type="checkbox" v-model="item.done">
        {{item.content}}
      </li>
    </ul>
    <button
      v-if="!(items.reduce((acc, cur)=> { return acc + !cur.done}, !items[0].done))"
      @click="removeItems"
    >Reset</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function() {
    return {
      items: [
        {
          id: 0,
          content: "Bread",
          done: false
        },
        {
          id: 1,
          content: "Milk",
          done: false
        },
        {
          id: 2,
          content: "Eggs",
          done: false
        },
        {
          id: 3,
          content: "Salt",
          done: false
        }
      ]
    };
  },
  methods: {
    toggleDone: function(index) {
      //console.log(this.items[index]);
      this.items[index].done = !this.items[index].done;
    },
    removeItems: function() {
      this.items.forEach(item => (item.done = false));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
.done {
  text-decoration: line-through;
}
.container {
  margin-left: 30px;
}
</style>
