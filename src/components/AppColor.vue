<template>
  <div>
    <form>
      <input
        type="number"
        placeholder="Enter color ID"
        v-model="search"
        v-on:keyup="getfilteredData"
      />
    </form>
    <div id="checkboxes" style="display:flex; flex-direction:row;">
      <div v-for="(brand, index) in brands" :key="index">
        <input type="checkbox" v-model="brand.checked" v-on:change="getfilteredData" />
        <label>{{ brand.value }}</label>
      </div>
    </div>

    <div class="card-columns" style="display:flex; flex-direction:row;">
      <template v-for="(item, index) in filteredData">
        <item-card :key="index" :item="item"></item-card>
      </template>
    </div>
  </div>
</template>

<script>
import ItemCard from "./ItemCard";
import data from "../data/data";
export default {
  name: "AppColor",
  components: {
    "item-card": ItemCard
  },
  computed: {
    selectedFilters: function() {
      let filters = [];
      let checkedFilters = this.brands.filter(obj => obj.checked);
      checkedFilters.forEach(element => {
        filters.push(element.value);
      });
      return filters;
    }
  },
  data() {
    return {
      filteredData: [],
      search: "",
      brands: [
        {
          checked: false,
          value: "RAL"
        },
        {
          checked: false,
          value: "Levis"
        },
        {
          checked: false,
          value: "Flexa"
        }
      ]
    };
  },
  methods: {
    getfilteredData: function() {
      this.filteredData = data;
      let filteredDataByFilters = [];
      let filteredDataBySearch = [];
      // Step 1. check if filters where selected?
      if (this.selectedFilters.length > 0) {
        filteredDataByFilters = this.filteredData.filter(obj =>
          this.selectedFilters.every(val => obj.brand.indexOf(val) >= 0)
        );
        this.filteredData = filteredDataByFilters;
      }
      // Step 2. filter according to typed id, this only affects the name attribute of each data
      if (this.search !== "") {
        filteredDataBySearch = this.filteredData.filter(
          obj => obj.name.indexOf(this.search.toLowerCase()) >= 0
        );
        this.filteredData = filteredDataBySearch;
      }
    }
  },
  mounted() {
    this.getfilteredData();
  }
};
</script>
