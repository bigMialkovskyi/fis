<template>
  <button @click="deselectRows">deselect rows</button>
  <ag-grid-vue
    class="ag-theme-alpine"
    style="height: 500px"
    :columnDefs="columnDefs"
    :rowData="rowData"
    :defaultColDef="defaultColDef"
    rowSelection="multiple"
    animateRows="true"
  >
  </ag-grid-vue>
</template>

<script>
import { AgGridVue } from "ag-grid-vue3"; // the AG Grid Vue Component
import { reactive, onMounted, ref } from "vue";

import "ag-grid-community/styles/ag-grid.css"; // Core grid CSS, always needed
import "ag-grid-community/styles/ag-theme-alpine.css"; // Optional theme CSS

export default {
  name: "App",
  components: {
    AgGridVue,
  },

  data() {
    return {
      columnDefs: [],
      rowData: [],
      defaultColDef: {
        sortable: true,
        filter: true,
        flex: 1,
      },
    };
  },

  mounted() {
    this.setColumns();

    this.rowData = this.createRandData();
  },

  methods: {
    setColumns() {
      this.columnDefs = [
        { field: "val1" },
        { field: "val2" },
        { field: "val3" },
        { field: "val4" },
        { field: "val5" },
        { field: "val6" },
        { field: "val7" },
        { field: "val8" },
      ];
    },

    createRandData() {
      function generateRandomString() {
        const characters =
          "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        let randomString = "";
        for (let i = 0; i < 10; i++) {
          randomString += characters.charAt(
            Math.floor(Math.random() * characters.length)
          );
        }
        return randomString;
      }

      function generateRandomFloat(min, max, decimal) {
        return (Math.random() * (max - min) + min).toFixed(decimal);
      }

      function generateRandomInt(min, max) {
        return Math.floor(Math.random() * (max - min + 1)) + min;
      }

      function generateRandomImagePath() {
        const imagePaths = [
          "images/image1.jpg",
          "images/image2.jpg",
          "images/image3.jpg",
          "images/image4.jpg",
          "images/image5.jpg",
        ];
        const randomIndex = Math.floor(Math.random() * imagePaths.length);
        return imagePaths[randomIndex];
      }

      function getRanomStringInArr() {
        const imagePaths = ["str1", "str2", "str3", "str4", "str5"];
        const randomIndex = Math.floor(Math.random() * imagePaths.length);
        return imagePaths[randomIndex];
      }
      let randContent = [];

      for (let i = 0; i < 100; i++) {
        randContent.push({
          val1: generateRandomString(),
          val2: Number(generateRandomFloat(1, 100, 2)),
          val3: Number(generateRandomFloat(1, 100, 4)),
          val4: generateRandomInt(0, 1000),
          val5: generateRandomInt(0, 1000),
          val6: generateRandomImagePath(),
          val7: generateRandomString(),
          val8: getRanomStringInArr(),
        });
      }
      // console.log(randContent);
      return randContent;
    },
  },
};
</script>

<style lang="scss"></style>