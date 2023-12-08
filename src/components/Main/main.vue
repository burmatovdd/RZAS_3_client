<template>
<header class="header">
  <sidebar/>
</header>
  <div class="main__container">
    <adder/>
    <dashboard/>
  </div>
</template>

<script>
import {defineComponent} from 'vue';
import sidebar from "../Sidebar/sidebar.vue";
import adder from "../Adder/adder.vue";
import dashboard from "../dashboard/dashboard.vue";

export default defineComponent( {
  name: "custom-main",
  components: {
    sidebar,
    adder,
    dashboard
  }

})
</script>

<style lang="scss">
@use 'main';
</style>