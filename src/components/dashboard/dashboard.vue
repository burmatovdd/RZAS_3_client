<template>
<div class="dashboard">
  <div class="dashboard__container">
    <div class="container__numbers">
      <numbers :title="'Количество записей'" :number="this.resources" class="container__number"/>
      <numbers :title="'Активные ресурсы'" :number="this.active" class="container__number"/>
      <numbers :title="'Неактивные ресурсы'" :number="this.resources-this.active" class="container__number"/>
    </div>
    <div class="container__table">
      <customTable/>
    </div>
  </div>
</div>
</template>

<script>
import {defineComponent} from 'vue';
import numbers from "../numbers/numbers.vue";
import customTable from "../Table/table.vue";
import * as httpClient from "../../../httpClient.js";

export default defineComponent({
  name: "dashboard",
  components: {
    numbers,
    customTable,
  },
  data: function () {
    return {
      resources: 0,
      waf: 0,
      ssl: 0,
      active: 0
    }
  },
  mounted() {
    let sendUrl = "http://localhost:8083/get-counter"
    httpClient.Get(sendUrl).then(response =>{
      this.resources = response.data.body.resources
      this.waf = response.data.body.waf
      this.ssl = response.data.body.ssl
      this.active = response.data.body.active
    })
  }
})
</script>

<style lang="scss">

@use "dashboard";
</style>