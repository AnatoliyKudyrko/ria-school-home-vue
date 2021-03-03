<template>
  <table class="table">
    <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Name</th>
      <th scope="col">Email</th>
      <th scope="col">Age</th>
    </tr>
    </thead>
     <UserListItem v-for="(user, index) of users" v-bind:user = user v-bind:index = index  />
  </table>
</template>

<script>
import UserListItem from "@/components/UserListItem";
export default {
name: "UserList",
  components: {UserListItem},
  props: ['users']
}
</script>

<style scoped>

</style>