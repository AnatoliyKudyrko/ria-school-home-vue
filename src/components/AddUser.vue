<template>
  <div>
    <Error v-if="errors.length >=1" v-bind:errors = 'errors'/>
    <form @submit.prevent="">
      <div class="row g-3">
        <div class="col-sm-5">
          <input type="text" class="form-control" maxlength=50 placeholder="Your Name"  v-model="yourName">
        </div>
        <div class="col-sm-5">
          <input type="text" class="form-control"  maxlength=50 placeholder="Your Email"  @blur="validEmail" v-model="mail">
        </div>
        <div class="col-sm">
          <input  type="number" min="1" class="form-control" placeholder="Your Age" v-model="age" >
        </div>
      </div>
      <br>
      <div class="col">
        <button  type="submit" class="btn btn-primary"
                 @click='addUser'
                 v-bind:class="[ (Object.keys(user).length === 3) && errors.length === 0 && user.age !== '' ? '' :  'disabled']">
          Add User</button>
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
      yourName: '',
      mail: '',
      age: '',
      user: {}
    }

  },

  watch: {
    yourName: function (val) {
      let errorText = "yourName: 'Повинно бути до 20 симфолів'";
      if (val.length < 20) {
        this.yourName = val;
        this.user.yourName = this.yourName;
        this.checkError(errorText)
      } else {
        this.checkError(errorText);

        if(this.checkError(errorText) === -1 ){
          this.errors.push(errorText);
        }

      }
    },

    age: function (val) {
      let errorText = "age: 'Повинно бути до 3 симфолів'";
      if (val.length < 3) {
        this.age = val;
        this.user.age = this.age;
        this.checkError(errorText);
      } else {
        this.checkError(errorText);

        if(this.checkError(errorText) === -1 ){
          this.errors.push(errorText);
        }

      }
    }
  },
  components: {Error},
  methods: {
    //повертає індекс помилки та видаляє помилку якщо поле відредактовано
    checkError(errorType) {
      let index = this.errors.indexOf(errorType);
      if (index !== -1) {
        this.errors.splice(index, 1);
        return;
      }
      return index;
    }
,
    addUser () {
      this.$emit('addUser', this.user);
      this.user = {}
      this.mail = '';
      this.yourName = '';
      this.age = '';
      this.errors = [];
    },
    validEmail () {
      let errorText = "mail: 'Перевірте написання потчи'";
      this.checkError(errorText);
      if (!(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.mail)) && this.checkError(errorText) === -1 ) {
        this.errors.push(errorText)
      }
      this.user.mail = this.mail;

    }
  },

}
</script>

<style scoped>

</style>