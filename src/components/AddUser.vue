<template>
  <div>
    <Error v-if="errors.length >=1" v-bind:errors = 'errors'/>
    <form @submit.prevent="onSubmit">
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" class="form-control" placeholder="Your Name"  v-model="yourName">
        </div>
        <div class="col-sm-5">
          <input type="text" class="form-control"   placeholder="Your Email"  @blur="validEmail" v-model="mail">
        </div>
        <div class="col-sm">
          <input  type="number"  min="1" class="form-control" placeholder="Your Age" v-model="age" >
        </div>
      </div>
      <br>
      <div class="col">
        <button  class="btn btn-primary" @click='addUser'>Add User</button>
      </div>
    </form>
  </div>

</template>

<script>
import Error from "@/components/Error";

export default {
  name: "AddUser",
  data() {
    return {
      errors: [],
      yourName: null,
      mail: null,
      age: null,
      user: {}
    }

  },

  watch: {
    yourName: function (val) {
      if (val.length < 20) {
        this.yourName = val;
        this.user.yourName = this.yourName;
        this.errors = [];
      } else {
        this.errors.push('name not answer');
      }
    },
    age: function (val) {
      if (val.length < 3) {
        this.age = val;
        this.user.age = this.age;
        this.errors = [];
      } else {
        this.errors.push('age not answer');
      }
    }
  },
  components: {Error},
  methods: {
    onSubmit () {
    },
    addUser () {
      this.$emit('addUser', this.user)
    },
    validEmail () {
      if (!(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.mail))) {
        this.errors.push('Please enter a valid email address')
      }
      this.user.mail = this.mail;
    }
  },

}
</script>

<style scoped>
button:disabled
</style>