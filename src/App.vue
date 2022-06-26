<template>
  <div id="app">
    <label> Filter </label>
    <input v-model="search" type="text" />
    <table>
      <tr>
        <th>Categories</th>
      </tr>
      <tr v-for="(item, index) in filteredItems" :key="index">
        <td>
          {{ item }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      items: [],
      search: "",
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter((item) =>
        item.toLowerCase().includes(this.search.toLowerCase())
      );
    },
  },
  mounted() {
    axios.get("https://api.publicapis.org/categories").then((response) => {
      this.items = response.data.categories;
    });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
* {
  box-sizing: border-box;
}
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
  padding: 5px;
}
table {
  width: 100%;
  margin-top: 16px;
}
th {
  background-color: black;
  color: white;
  font-size: 1.125rem;
}
label {
  font-weight: 600;
}
input {
  border-radius: 4px;
}
</style>
