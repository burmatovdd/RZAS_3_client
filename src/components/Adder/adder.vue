<template>
  <div class="adder">
    <div class="adder__container">
      <input type="text" placeholder="domain..." class="adder__input" v-model="domain">
      <button class="adder__button" @click="openModal">Добавить новый ресурс</button>
    </div>
  </div>
  <modal v-if="isOpen" :domain="this.domain"/>
</template>

<script>
import {defineComponent} from 'vue';
import modal from "../modal/modal.vue";


export default defineComponent({
  name: "adder",
  components: {modal},
  data:  () => {
    return{
      isOpen: false,
      domain: ""
    }
  },
  methods:{
    openModal: function () {
      this.isOpen = !this.isOpen
    }
  }
})
</script>

<style lang="scss">
@use  'adder';
</style>