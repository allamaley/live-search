<template>
  <div class>
    <div class="colorCode" :style="{'background-color': item.hex}">
      <p>{{ item.name | capitalize }}</p>
      <div class="colorDetails">
        <div>{{item.brand}}</div>
        <div v-for="(group, index) in item.color" :key="index">Group: {{ group }}</div>
      </div>
      <div class="colorCode__productCode">{{item.hex}}</div>
    </div>
  </div>
</template>
<style>
.colorCode {
  position: relative;
  color: white;
  display: flex;
  flex-flow: column nowrap;
  min-height: 120px;
  width: 160px;
  margin: 15px;
  padding: 6px;
}
.colorDetails {
  display: flex;
  flex-flow: column nowrap;
  font-size: 14px;
}
.colorCode__productCode {
  font-size: 10px;
}
</style>
<script>
export default {
  filters: {
    capitalize: item => {
      return item.toUpperCase();
    }
  },
  props: {
    item: {
      type: Object,
      required: true
    }
  }
};
</script>

