<template>
  <div class="modal">
    <div class="modal__container">
      <input type="checkbox" id="waf" v-model="waf" class="checkbox">
      <label for="waf" class="label">Waf</label>
      <input type="checkbox" id="ssl" v-model="ssl" class="checkbox">
      <label for="ssl" class="label">SSL</label>
      <input type="checkbox" id="active" v-model="active" class="checkbox">
      <label for="active" class="label">Активный</label>
      <input type="text" placeholder="owner..." class="modal__input" v-model="owner">
      <button class="modal__button" @click="send">Добавить новый ресурс</button>

    </div>
  </div>
</template>

<script>
import {defineComponent} from 'vue';
import * as httpClient from "../../../httpClient.js";

export default defineComponent({
  name: "modal",
  props: {
    domain: ""
  },
  data: () => {
    return{
      waf: false,
      ssl: false,
      active: false,
      owner: "fallback content"
    }
  },
  methods: {
    send: function () {
      console.log(this.info)

      let data = {
        domain: this.$props.domain,
        waf: this.waf,
        ssl: this.ssl,
        active: this.active,
        owner: this.owner
      }

      console.log("data: ", data)

      let sendUrl = "http://localhost:8083/add-resource"
      return httpClient.Post(sendUrl, data).then(response => {
        console.log("response: ",response)
      })
    }
  }
})
</script>

<style lang="scss">
@use "modal";
</style>