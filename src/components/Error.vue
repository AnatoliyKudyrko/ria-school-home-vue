<template>
  <div class="alert alert-danger" role="alert">
    This is a danger alert—check it out!
    {{errors}}
  </div>
</template>

<script>
export default {
  name: "Error",
  props:["errors"]
}
</script>

<style scoped>

</style>