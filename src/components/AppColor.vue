<template>
  <div>
    <form class="filter">
      <input
        id="inputColorId"
        type="text"
        placeholder="Enter color ID"
        v-model="search"
        v-on:keyup="getfilteredData"
      />
    </form>
    <div id="checkboxes" class="filter">
      <div v-for="(color, index) in colors" :key="index">
        <label class="label-container">
          {{ color.value }}
          <input
            type="checkbox"
            v-model="color.checked"
            v-on:change="getfilteredData"
          />
          <span class="checkmark"></span>
        </label>
      </div>
    </div>
    <select id="brandList" class="filter" @change="getfilteredData($event)" v-model="selectedBrand">
      <option v-for="(brand, index) in brands" :value="brand" :key="index">{{ brand }}</option>
    </select>

    <div class="card-columns">
      <template v-for="(item, index) in filteredData">
        <item-card :key="index" :item="item"></item-card>
      </template>
    </div>
  </div>
</template>

<style>
.filter {
  margin: 1rem;
}
#checkboxes,
.card-columns {
  display: flex;
  flex-flow: row wrap;
}
/** Custom checkboxes **/
.label-container {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-right: 12px;
  cursor: pointer;
  font-size: 22px;
  user-select: none;
  transition: 0.5s;
}
.label-container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: #eee;
  transition: 0.5s;
}

.label-container:hover input ~ .checkmark {
  background-color: #ccc;
  transition: 0.5s;
}

.label-container input:checked ~ .checkmark {
  background-color: darkgray;
  transition: 0.5s;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.label-container input:checked ~ .checkmark:after {
  display: block;
}

.label-container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  transform: rotate(45deg);
}
/** Custom select **/
select {
  background: #ffffff;
  overflow: hidden;
  border: 1px solid #cbcbcb;
  border: none;
  padding: 10px 10px 10px 5px;
  text-overflow: "";
  text-indent: 5px;
  width: 20%;
  border-color: transparent;
  outline-color: transparent;
  transition: 0.5s;
}
input,
select {
  font-family: "Kulim Park", sans-serif;
}
/** Custom input **/
input#inputColorId {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: 2px solid #e1e1e1;
  transition: 0.5s;
  outline: none;
}

input#inputColorId:focus {
  border: 2px solid darkgray;
}
</style>
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
      let checkedFilters = this.colors.filter(obj => obj.checked);
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
      selectedBrand: "RAL",
      colors: [
        {
          checked: false,
          value: "green"
        },
        {
          checked: false,
          value: "beige"
        },
        {
          checked: false,
          value: "white"
        },
        {
          checked: false,
          value: "sand"
        }
      ],
      brands: ["RAL", "Levis", "Flexa"]
    };
  },
  methods: {
    getfilteredData: function(event) {
      if (event != undefined) {
        this.selectedBrand =
          event.target.id === "brandList"
            ? event.target.value
            : this.selectedBrand;
      }
      this.filteredData = data;
      let filteredDataByFilters = [];
      let filteredDataBySelect = [];
      let filteredDataBySearch = [];
      // Step 1. check if filters where selected?
      if (this.selectedFilters.length > 0) {
        filteredDataByFilters = this.filteredData.filter(obj =>
          this.selectedFilters.every(val => obj.color.indexOf(val) >= 0)
        );
        this.filteredData = filteredDataByFilters;
      }
      // Step 1.2 check if selector filters where selected?
      if (this.selectedBrand.length > 0) {
        //this.filteredData.forEach(obj => console.log(obj.brand));
        filteredDataBySelect = this.filteredData.filter(
          obj => obj.brand.indexOf(this.selectedBrand) >= 0
        );
        this.filteredData = filteredDataBySelect;
      }
      // Step 2. filter according to typed id, this only affects the name attribute of each data
      if (this.search !== "") {
        filteredDataBySearch = this.filteredData.filter(
          obj => obj.name.toLowerCase().indexOf(this.search.toLowerCase()) >= 0
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
