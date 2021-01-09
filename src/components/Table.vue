<template>
  <div class="main">
    <div class="search-box">
      <span>Search</span>
      <input v-model="searchText" type="text" @input="search" />
    </div>

    <div class="table-container">
      <div class="header">
        <h3>Category</h3>
      </div>
      <TableCell
        v-for="(category, index) in searchArray"
        :key="index"
        :name="category"
      ></TableCell>
    </div>
  </div>
</template>

<script>
import TableCell from "./TableCell";
import axios from "axios";
export default {
  name: "Table",
  components: { TableCell },
  data() {
    return {
      categories: [],
      searchText: "",
      searchArray: [],
    };
  },
  mounted() {
    this.fetchCategories();
  },
  methods: {
    async fetchCategories() {
      const result = await axios.get("https://api.publicapis.org/categories");
      this.categories = result.data;
      this.searchArray = this.categories;
    },
    search() {
      /** for better performance when search text empty use direct categories no need to do array filter */
      if (this.searchText === "") {
        this.searchArray = this.categories;
      } else {
        this.searchArray = this.categories.filter((cat) => {
          const found = cat
            .toLowerCase()
            .includes(this.searchText.toLowerCase());
          return found;
        });
      }
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  width: 100vw;
  align-items: center;
}
.search-box {
  margin-bottom: 16px;
  display: grid;
  grid-template-rows: auto;
  grid-template-columns: 1fr 1fr;
}

.table-container {
  width: 480px;
  display: grid;
  grid-template-rows: auto;
  grid-template-columns: 1fr;
  grid-auto-flow: row;
  grid-auto-rows: auto;
  border: 1px solid black;
  padding: 16px;
}
.header {
  border-bottom: 1px solid black;
  padding-bottom: 16px;
  margin-bottom: 8px;
}
.header > h3 {
  margin: 0;
}
</style>
