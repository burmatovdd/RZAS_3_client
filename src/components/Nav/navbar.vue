<template>
<nav class="nav">
  <ul class="nav__row">
    <li class="nav__item">
      <div class="nav__item-row">
        <button class="nav__item-row-btn" @click="checkDBVersion">
          <svg width="17" height="17" viewBox="0 0 17 17" fill="none" xmlns="http://www.w3.org/2000/svg" class="nav__img">
            <path d="M1 8.5L8.49204 12.25L16 8.5M1 12.25L8.49204 16L16 12.25M1 4.89719L8.49953 8.5L16 4.89719L8.49953 1L1 4.89719Z" stroke-width="0.952381" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
          <p class="nav__text">Версия базы данных</p>
        </button>
      </div>
    </li>
    <li class="nav__item">
      <div class="nav__item-row">
        <button class="nav__item-row-btn" @click="getDBSize">
          <svg width="15" height="15" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg" class="nav__img">
            <path d="M1.875 5.625V3.75C1.875 3.25272 2.07254 2.77581 2.42417 2.42417C2.77581 2.07254 3.25272 1.875 3.75 1.875H11.25C11.7473 1.875 12.2242 2.07254 12.5758 2.42417C12.9275 2.77581 13.125 3.25272 13.125 3.75V11.25C13.125 11.7473 12.9275 12.2242 12.5758 12.5758C12.2242 12.9275 11.7473 13.125 11.25 13.125H9.375"  stroke-width="1.66667" stroke-linecap="round"/>
            <path d="M10 5V4.375H10.625V5H10ZM6.37938 9.50437C6.26151 9.61822 6.10363 9.68122 5.93976 9.6798C5.77589 9.67837 5.61913 9.61264 5.50325 9.49676C5.38737 9.38088 5.32164 9.22412 5.32021 9.06025C5.31879 8.89638 5.38179 8.7385 5.49564 8.62062L6.37938 9.50437ZM9.37501 8.75V5H10.625V8.75H9.37501ZM10 5.625H6.25001V4.375H10V5.625ZM10.4419 5.44187L6.37938 9.50437L5.49564 8.62062L9.55813 4.55813L10.4419 5.44187Z" fill="#757DA2"/>
            <path d="M5 8.75H3.125C2.43464 8.75 1.875 9.30964 1.875 10V11.875C1.875 12.5654 2.43464 13.125 3.125 13.125H5C5.69036 13.125 6.25 12.5654 6.25 11.875V10C6.25 9.30964 5.69036 8.75 5 8.75Z"  stroke-width="1.66667" stroke-linecap="round"/>
          </svg>
          <p class="nav__text">Размер базы данных</p>
        </button>
      </div>
    </li>
    <li class="nav__item">
      <div class="nav__item-row">
        <button class="nav__item-row-btn" @click="getTbSize">
          <svg width="15" height="15" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1.25 2.34375C1.25 1.74 1.74 1.25 2.34375 1.25H12.6562C13.26 1.25 13.75 1.74 13.75 2.34375V12.6562C13.75 12.9463 13.6348 13.2245 13.4296 13.4296C13.2245 13.6348 12.9463 13.75 12.6562 13.75H2.34375C2.05367 13.75 1.77547 13.6348 1.57035 13.4296C1.36523 13.2245 1.25 12.9463 1.25 12.6562V2.34375ZM5.625 5.625V12.8125H12.6562C12.6977 12.8125 12.7374 12.796 12.7667 12.7667C12.796 12.7374 12.8125 12.6977 12.8125 12.6562V5.625H5.625ZM12.8125 4.6875V2.34375C12.8125 2.30231 12.796 2.26257 12.7667 2.23326C12.7374 2.20396 12.6977 2.1875 12.6562 2.1875H5.625V4.6875H12.8125ZM2.1875 5.625V12.6562C2.1875 12.7425 2.2575 12.8125 2.34375 12.8125H4.6875V5.625H2.1875ZM4.6875 4.6875V2.1875H2.34375C2.30231 2.1875 2.26257 2.20396 2.23326 2.23326C2.20396 2.26257 2.1875 2.30231 2.1875 2.34375V4.6875H4.6875Z" fill="#757DA2"/>
          </svg>
          <p class="nav__text">Размер таблиц</p>
        </button>
      </div>
    </li>
  </ul>
</nav>
</template>

<script>
import {defineComponent} from 'vue';
import * as httpClient from "../../../httpClient.js";
export default defineComponent({
  name: "custom-nav",
  data: function () {
    return {
      tb: {
        size: ""
      },
      database:{
        size: "",
        version: ""
      },
    }
  },
  methods: {
    checkDBVersion: function () {
      let sendurl = "http://localhost:8083/get-db-version"
      httpClient.Get(sendurl).then(response =>{
        this.database.version = response.data.body
        alert("Версия базы данных: "+this.database.version)
      })
    },
    getDBSize: function () {
      let sendurl = "http://localhost:8083/get-db-size"
      httpClient.Get(sendurl).then(response =>{
        this.database.size = response.data.body
        alert("Размер базы данных: "+this.database.size)
      })
    },
    getTbSize: function () {
      let sendurl = "http://localhost:8083/get-tb-size"
      httpClient.Get(sendurl).then(response =>{
        console.log(response.data.body)
        this.tb.size = response.data.body
        alert("Размер таблицы: "+this.tb.size)
      })
    },
  }
})
</script>

<style lang="scss">
@use  'nav';
</style>