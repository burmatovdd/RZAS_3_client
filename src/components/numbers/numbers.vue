<template>
  <div class="block">
    <div class="block__container">
      <p class="block__container-title">{{$props.title}}</p>
      <div class="block__container-number">{{$props.number}}</div>
    </div>
  </div>

</template>

<script>
export default {
  name: "numbers",
  props:{
    title: "",
    number: 0
  }
}
</script>

<style lang="scss">
@use 'numbers';
</style>