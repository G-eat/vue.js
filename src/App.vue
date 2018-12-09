<template>
  <div id="app" class="container">
    <h4 v-if='updateUser.email'>Update user</h4>
    <h4 v-else>Add User</h4>
    <hr style="border: 1px solid rgba(0, 0, 0, 0.5;">
    <Create @create="newUser" @update='updated' v-bind:update=updateUser />
    <!-- <Home msg='123' /> -->
    <br>
    <hr style="border: 1px solid rgba(0, 0, 0, 0.5;">
    <h4>All users</h4>
    <ul id='small' class="row">
      <li class="collection left-align" v-for='(user , index) in users' :key="user.on">
        <span v-if='user.on'>
          <div class="switch col s12 m3 l3 qender">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox" checked="checked">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>On</span>
            </label>
          </div>
        </span>
        <span v-else>
          <div class="switch col s12 m3 l3 qender">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>On</span>
            </label>
          </div>
        </span>
        <div v-if='user.on' v-bind:style='{ color : color }' @click='update(user ,index)' class="qender">{{ user.userName }} - {{ user.email}}</div>
        <div v-else @click='update(user, index)' class="qender">{{ user.userName }} - {{ user.email}}</div>
        <div style="cursor:pointer; width:40%; float:right; color:white; margin:10px 40px 20px 5px" class="new badge red darken-4 collection-item" data-badge-caption="" @click='deleteUser(index)'>Delete</div>
        <div v-bind:class="{ blue: user.gender == 'Male' }" style="width:40%; float:right; color:white; margin:10px 0 20px 0" class="new badge red tooltipped collection-item" data-badge-caption="age">{{user.age}}</div>
      </li>
    </ul>

    <ol id='medium-large' class="collection row">
      <li class="collection-item left-align" v-for='(user , index) in users' :key="user.on">
        <span v-if='user.on'>
          <span id="special1" class="switch col s12 m3 l3">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox" checked="checked">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>On</span>
            </label>
          </span>
        </span>
        <span v-else>
          <span id="special1" class="switch col s12 m3 l3">
            <label>
              <span @click='onOff(index,user.userName)'>Off</span>
              <input type="checkbox">
              <span @click='onOff(index,user.userName)' class="lever"></span>
              <span @click='onOff(index,user.userName)'>On</span>
            </label>
          </span>
        </span>
        <span v-if='user.on' v-bind:style='{ color : color }' @click='update(user ,index)' id="special2" class="col s12 m6 l6">{{ user.userName }} - {{ user.email}}</span>
        <span v-else @click='update(user, index)' id="special2" class="col s12 m6 l6">{{ user.userName }} - {{ user.email}}</span>
        <span style="cursor:pointer" id="special3" class="new badge red darken-4" data-badge-caption="" @click='deleteUser(index)'>Delete</span>
        <span v-bind:class="{ blue: user.gender == 'Male' }" id="special3" class="new badge red tooltipped" data-badge-caption="age">{{user.age}}</span>
        <br><br>
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

@media only screen and (max-width: 800px) {
    #special1 {
        width: 33%;
    }

    #special2 {
      width: 65%;
    }

    #special3 {
      width:22%;
    }

    #medium-large {
      display: none;
    }
}

@media only screen and (min-width: 801px) {
  #small {
    display: none;
  }
}

@media only screen and (max-width: 602px) {
  .qender {
    text-align: center;
  }
}

</style>
