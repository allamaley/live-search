<template>
  <div id="app" class="container mx-auto py-6">
    <div class="content">
      <AppColor />
    </div>
  </div>
</template>

<script>
import AppColor from "./components/AppColor.vue";

export default {
  name: "app",
  components: {
    AppColor
  }
};
</script>