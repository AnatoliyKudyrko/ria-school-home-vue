<template>
  <tbody>
  <tr>
    <th scope="row">{{index+1}}</th>
    <td>{{user.yourName | uppercase}}</td>
    <td>{{user.mail}}</td>
    <td>{{user.age}}</td>
  </tr>
  </tbody>
</template>

<script>
export default {
  name: "UserListItem.vue",
  props: ['user','index'],
  filters: {
    uppercase(value){
      return value.toUpperCase();
    }
  }
}
</script>

<style scoped>

</style>