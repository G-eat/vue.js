<template lang="html">
  <div class="">
    <div v-if="err != ''" class='card-panel red accent-4 white-text'>{{ err }}</div>
    <div v-if="succ != ''" class='card-panel green accent-4 white-text'>{{ succ }}</div>
    <form v-if="!update.email" class="col s12" @submit.prevent='newUser'>
      <div class="row">
        <div class="input-field col s12 m6 l6">
          <input  type="text" name="newUser" v-model='input' placeholder="New User">
        </div>
        <div class="input-field col s12 m6 l6">
          <input  type="email" name="email" v-model='email' placeholder="User Email">
        </div>
        <div class="input-field col s12 m5 15">
          <select v-model='gender' class="browser-default">
            <option disabled selected>{{ gender }}</option>
            <option>Male</option>
            <option>Female</option>
          </select>
        </div>
        <div class="input-field col s12 m5 l5">
          <input type="number" name="age" v-model='age' placeholder="Age">
        </div>
        <div class="input-field col s12 m12 l2">
          <button type="submit" class='waves-effect waves-light btn col s12' name="button">Submit</button>
        </div>
      </div>
    </form>

    <div v-else>
      <form class="col s12" @submit.prevent='updateUser'>
        <div class="row">
          <div class="input-field col s12 m6 l6">
            <input type="text" name="updateUser" placeholder="New User" :value="update.userName">
          </div>
          <div class="input-field col s12 m6 l6">
            <input type="email" name="updateemail" placeholder="User Email" :value="update.email">
          </div>
          <div class="input-field col s12 m5 l5">
            <select class="browser-default">
              <option disabled selected>{{ update.gender }}</option>
            </select>
          </div>
          <div class="input-field col s12 m5 l5">
            <input type="number" name="updateage" placeholder="Age" :value="update.age">
          </div>
          <div class="input-field col s12 m12 l2">
            <input type="hidden" name="index" :value="update.index">
            <button type="submit" class='waves-effect waves-light btn col s12' name="updatebutton">Update</button>
          </div>
        </div>
      </form>
      <button style="width:100%" @click='cancel' type="submit" class='waves-effect waves-light btn grey' name="cancel">Cancel</button>
      <br>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    update: Object
  },
  data (){
    return {
      input : '',
      email : '',
      age : '',
      gender : 'Gender',
      err : '',
      succ : ''
    }
  },
  methods: {
    newUser (e) {
      if (e.target.newUser.value.trim().length > 0 && this.email != '' && (this.age >= 16 && this.age <= 80) && this.gender != 'Gender') {
        this.$emit('create',{ userName : e.target.newUser.value , email : this.email , age : this.age , gender : this.gender , on : false });
        this.succ = 'You created a New User !';
        this.input = '';
        this.email = '';
        this.age = '';
        this.gender = 'Gender';
        this.err = '';
      } else {
          this.err = "Complite Form.Error!";
      }
      this.$nextTick(function () {
          window.setInterval(() => {
              this.countDown();
          },5000);
      });
    },
    countDown() {
      this.err = '';
      this.succ = '';
    },
    updateUser(e) {
      if (e.target.updateUser.value.trim().length > 0 && e.target.updateemail.value != '' && (e.target.updateage.value >= 16 && e.target.updateage.value <= 80)) {
        this.$emit('update',{ userName : e.target.updateUser.value , email : e.target.updateemail.value , age : e.target.updateage.value , gender : this.update.gender , index: e.target.index.value , on:this.update.on});
        this.succ = 'You updated a User !';
        this.update.email = '';
        this.$nextTick(function () {
          window.setInterval(() => {
            this.countDown();
          },5000);
        });
      } else {
        this.err = "Complite Form.Error !";
        this.succ = '';
        this.$nextTick(function () {
            window.setInterval(() => {
                this.countDown();
            },5000);
        });
      }
    },
    cancel() {
      this.update.email = '';
    }
  }
}
</script>

<style lang="css">
</style>
