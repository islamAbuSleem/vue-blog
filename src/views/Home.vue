<template>
  <div class="contain">
    <ag-grid-vue
      style="height: 200px"
      class="ag-theme-alpine"
      :pagination="true"
      :paginationPageSize="paginationPageSize"
      :columnDefs="columnDefs"
      :rowData="rowData"
      @row-clicked="goToPost($event)"
    >
    </ag-grid-vue>
  </div>
</template>

<script>
import axios from "axios";
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue3";

export default {
  name: "App",
  components: {
    AgGridVue,
  },
  props: ["post"],
  data() {
    return {
      columnDefs: [
        { headerName: "userId", field: "userId" },
        { headerName: "id", field: "id" },
        { headerName: "title", field: "title" },
      ],
      rowData: [],
      paginationPageSize: 10,
    };
  },
  created() {
    this.getPosts();
  },
  methods: {
    async getPosts() {
      try {
        const returnPosts = await axios.get(
          " https://jsonplaceholder.typicode.com/posts"
        );
        this.rowData = returnPosts.data;
      } catch (e) {
        console.log(e.messge);
      }
    },
    goToPost(cell) {
      // alert('clicked '+ cell.data.id)
      this.$router.push({ name: "post", params: { id: cell.data.id } });
    },
  },
};
</script>

<style lang="scss">
.ag-theme-alpine {
  height: 550px !important;
  width: 600px;
  margin: 3% auto;
}
</style>