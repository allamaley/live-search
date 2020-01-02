<template>
  <div id="app" class="container mx-auto py-6">
    <div class="content">
      <AppColor />
    </div>
  </div>
</template>
<style>
@import url("https://fonts.googleapis.com/css?family=Kulim+Park&display=swap");
body {
  font-family: "Kulim Park", sans-serif !important;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.content {
  margin: 0 auto;
  width: 820px;
  min-height: 600px;
  background: #80808014;
  border-radius: 0.5rem;
  padding: 2rem;
  box-shadow: 0 0 30px rgba(16, 14, 23, 0.25);
}
</style>
<script>
import AppColor from "./components/AppColor.vue";

export default {
  name: "app",
  components: {
    AppColor
  }
};
</script>