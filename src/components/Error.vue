<template>
  <div class="alert alert-danger error" role="alert">
    Помилка введення у полях
    <ul>
      <li v-for="item in errors" :key="item">
        {{ item }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Error",
  props:["errors"]
}
</script>

<style scoped>
.error{
  display: flex;
}
ul{
  display: flex;
  flex-direction: row;
  list-style: none;
}
li{
  padding-left: 20px;
}
</style>