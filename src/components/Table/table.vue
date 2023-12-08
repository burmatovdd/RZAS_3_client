<template>
<div class="table">
  <div class="table__container">
    <table class="container__tbl">
      <tr class="tr">
        <th class="th th__domain">Ресурс</th>
        <th class="th">Статус активности</th>
        <th class="th th__owner">Владелец</th>
      </tr>
      <tr class="tr" v-for="item in result">
        <th class="th th__domain">{{item.domain}}</th>
        <th class="th th__active">{{item.active}}</th>
        <th class="th th__owner">{{item.owner}}</th>
      </tr>
    </table>
    <button class="table__button-edit" @click="isClickEdit = !isClickEdit">
      <svg width="21" height="20" viewBox="0 0 21 20" fill="none" xmlns="http://www.w3.org/2000/svg" class="table__button-img">
        <g clip-path="url(#clip0_101_86)">
          <path d="M13.7637 2.51248C14.2119 2.06364 14.8138 1.80228 15.4474 1.78139C16.0809 1.76049 16.6987 1.98164 17.1754 2.39998L17.2952 2.51248L17.8837 3.10165C18.3317 3.55033 18.5926 4.1528 18.6135 4.78693C18.6343 5.42106 18.4136 6.03941 17.996 6.51665L17.8837 6.63665L8.55182 15.9808C8.41988 16.1129 8.26004 16.2137 8.08406 16.2758L7.94923 16.315L4.24212 17.1716C4.11225 17.2017 3.97708 17.2001 3.84795 17.167C3.71882 17.1339 3.59951 17.0703 3.50003 16.9815C3.40055 16.8926 3.32381 16.7812 3.27625 16.6565C3.22869 16.5319 3.2117 16.3976 3.2267 16.265L3.24335 16.1708L4.09813 12.4583C4.14036 12.2762 4.22284 12.1059 4.3395 11.96L4.43189 11.8558L13.7637 2.51248ZM13.1753 5.45831L5.69284 12.95L5.16349 15.2483L7.459 14.7175L14.9415 7.22581L13.1753 5.45831ZM16.1183 3.69081C15.975 3.54733 15.7843 3.46114 15.5821 3.44841C15.3798 3.43567 15.1798 3.49727 15.0197 3.62165L14.9415 3.69081L14.3522 4.27998L16.1183 6.04748L16.7068 5.45831C16.8501 5.31482 16.9362 5.1239 16.9489 4.92138C16.9616 4.71886 16.9001 4.51865 16.7759 4.35831L16.7068 4.27998L16.1183 3.69081Z" fill="white"/>
        </g>
        <defs>
          <clipPath id="clip0_101_86">
            <rect width="19.9754" height="20" fill="white" transform="translate(0.417664)"/>
          </clipPath>
        </defs>
      </svg>
    </button>
    <button class="table__button-remove" @click="isClickRemove = !isClickRemove">
      <svg width="15" height="16" viewBox="0 0 15 16" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M9.00614 7.16667V12.1667M5.6769 7.16667V12.1667M2.34766 3.83333V13.8333C2.34766 14.2754 2.52304 14.6993 2.83522 15.0118C3.1474 15.3244 3.5708 15.5 4.01228 15.5H10.6708C11.1122 15.5 11.5356 15.3244 11.8478 15.0118C12.16 14.6993 12.3354 14.2754 12.3354 13.8333V3.83333M0.683044 3.83333H14M3.17997 3.83333L4.84459 0.5H9.83845L11.5031 3.83333" stroke="white" stroke-width="0.833333" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </button>
  </div>
  <div class="remove edit" v-if="this.isClickEdit">
    <input type="text" placeholder="domain..." class="table__input table__input-domain" v-model="domain">
    <input type="checkbox" id="waf" v-model="waf" class="checkbox">
    <label for="waf" class="label">Waf</label>
    <input type="checkbox" id="ssl" v-model="ssl" class="checkbox">
    <label for="ssl" class="label">SSL</label>
    <input type="checkbox" id="active" v-model="active" class="checkbox">
    <label for="active" class="label">Активный</label>
    <input type="text" placeholder="owner..." class="table__input" v-model="owner">
    <button class="table__button table__button-edit" @click="edit">Обновить ресурс</button>
  </div>
  <div class="remove" v-if="this.isClickRemove">
    <input type="text" placeholder="owner..." class="table__input" v-model="domain">
    <button class="table__button" @click="remove">Удалить ресурс</button>
  </div>

</div>
</template>

<script>
import {defineComponent} from 'vue';
import * as httpClient from "../../../httpClient.js";


export default defineComponent({
  name: "custom-table",
  data: () => {
    return{
      result: [],
      domain: "",
      isClickRemove: false,
      isClickEdit: false,
      waf: false,
      ssl: false,
      active: false,
      owner: "",
    }
  },
  methods:{
    remove: function () {
      this.isClick = !this.isClick
      let sendUrl = "http://localhost:8083/delete-resource"
      return httpClient.Post(sendUrl, this.domain).then(response => {
        console.log("response: ",response)
      })
    },
    edit: function () {
      this.isClickEdit = !this.isClickEdit
      let data = {
        domain: this.domain,
        waf: this.waf,
        ssl: this.ssl,
        active: this.active,
        owner: this.owner
      }
      console.log(data)
      let sendUrl = "http://localhost:8083/edit-resource"
      return httpClient.Post(sendUrl, data).then(response => {
        console.log("response: ",response)
      })

    }
  },
  mounted() {
    let sendurl = "http://localhost:8083/get-info"
    httpClient.Get(sendurl).then(response =>{
      this.result = response.data.body
    })
  }

})
</script>

<style lang="scss">
@use "table";
</style>