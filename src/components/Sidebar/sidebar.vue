<template>
<div class="sidebar">
  <div class="sidebar__row">
    <div class="sidebar__title">
      <h3 class="title">Burmatov App</h3>
    </div>
    <navbar/>
  </div>
  <p class="sidebar__info">Работу выполнил студент группы БББО-07-20</p>
</div>
</template>

<script>
import {defineComponent} from 'vue';
import navbar from "../Nav/navbar.vue";

export default defineComponent( {
  name: "sidebar",
  components: {
    navbar
  }
})
</script>

<style lang="scss">
@use 'sidebar';
</style>