<template>
  <div class>
    <div class="colorCode" :style="{'background-color': item.hex}">
      <h2>{{ item.name | capitalize }}</h2>
      <div class="colorCode__productCode">{{item.hex}}</div>
      <div>
        <span v-for="(group, index) in item.brand" :key="index">{{ group }}</span>
      </div>
    </div>
  </div>
</template>
<style>
.colorCode {
  position: relative;
  color: white;
  display: flex;
  flex-direction: row;
  height: 70px;
  width: 160px;
  margin: 15px;
}
.colorCode__productCode {
  position: absolute;
  bottom: 10px;
  right: 10px;
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

