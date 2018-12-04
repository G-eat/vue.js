<template lang="html">
  <div class="">
    <div v-if="err != ''" class='card-panel red accent-4 white-text'>{{ err }}</div>
    <form class="col s12" @submit.prevent='newUser'>
      <div class="row">
        <div class="input-field col s6">
          <input type="text" name="newUser" v-model='input' placeholder="New User">
        </div>
        <div class="input-field col s6">
          <input type="email" name="email" v-model='email' placeholder="User Email">
        </div>
        <div class="input-field col s5">
          <select v-model='gender' class="browser-default">
            <option disabled selected>{{ gender }}</option>
            <option>Male</option>
            <option>Female</option>
          </select>
        </div>
        <div class="input-field col s5">
          <input type="number" name="age" v-model='age' placeholder="Age">
        </div>
        <div class="input-field col s2">
          <button type="submit" class='waves-effect waves-light btn' name="button">Submit</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data (){
    return {
      input : '',
      email : '',
      age : '',
      gender : 'Gender',
      err : ''
    }
  },
  methods: {
    newUser (e) {
      if (e.target.newUser.value.trim().length > 0 && this.email != '' && (this.age >= 16 && this.age <= 80) && this.gender != 'Gender') {
        this.$emit('create',{ userName : e.target.newUser.value , email : this.email , age : this.age , gender : this.gender , on : false });
        this.input = '';
        this.email = '';
        this.age = '';
        this.gender = 'Gender';
        this.err = '';
      } else {
        this.err = "You need to compelte the form !";
        this.$nextTick(function () {
            window.setInterval(() => {
                this.countDown();
            },5000);
        });
      }
    },
    countDown() {
      this.err = '';
    }
  }
}
</script>

<style lang="css">
</style>
