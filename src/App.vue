<template>
  <div id="app" class="container">
    <h4 v-if='updateUser.email'>Update user</h4>
    <h4 v-else>Add User</h4>
    <hr style="border: 1px solid rgba(0, 0, 0, 0.5;">
    <Create @create="newUser" @update='updated' v-bind:update=updateUser />
    <!-- <Home msg='123' /> -->
    <hr style="border: 1px solid rgba(0, 0, 0, 0.5;">
    <h4>All users</h4>
    <ol class="collection">
      <li class="collection-item left-align" v-for='(user , index) in users' :key="user.on">
        <span v-if='user.on'>
          <span class="switch">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox" checked="checked">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>Contacted</span>
            </label>
          </span>
        </span>
        <span v-else>
          <span class="switch">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>Contacted</span>
            </label>
          </span>
        </span>
        <span v-if='user.on' v-bind:style='{ color : color }' @click='update(user ,index)'>{{ user.userName }} - {{ user.email}}</span>
        <span v-else @click='update(user, index)'>{{ user.userName }} - {{ user.email}}</span>
        <span style="cursor:pointer" class="new badge red darken-4" data-badge-caption="" @click='deleteUser(index)'>Delete</span>
        <span v-bind:class="{ blue: user.gender == 'Male' }" class="new badge red tooltipped" data-badge-caption="age">{{user.age}}</span>
      </li>
    </ol>
  </div>
</template>

<script>
 // import Home from './components/Home.vue'
 import Create from './components/Create.vue'

export default {
  name: 'app',
  components: {
     // Home,
     Create
  },
  data (){
    return {
      users : [
        {
          userName: 'Andi',
          email : 'andi@gmail.com',
          age : 22,
          gender : 'Male',
          on : false
        }
      ],
      updateUser : '',
      color : 'green'
    }
  },
  methods : {
    newUser (e) {
      this.users.push(e);
    },
    onOff(i){
        this.users[i].on = !this.users[i].on;
    },
    deleteUser(i) {
      this.users.splice(i,1);
    },
    update(u ,i) {
      this.updateUser = { userName :u.userName , email :u.email , age :u.age , gender :u.gender , index :i , on :u.on};
    },
    updated(e) {
      this.users.splice(e.index,1);
      this.users.push(e);
    }
  }
}

</script>

<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/materialize/1.0.0/css/materialize.min.css');

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.switch {
  margin-right: 10px;
}
</style>
