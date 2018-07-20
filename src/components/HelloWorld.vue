<template>
  <div class="main">
    <div class="btn-toolbar">
      <button type="button" class=" btn btn-primary btn-md" v-on:click="addform"> ADD TODO </button>
      <button type="button" class="btn btn-default btn-md " v-on:click="showlist">TODO LIST</button>
      <br/>
      <div class="added">
        <h1>{{message}}</h1>
      </div>
    </div>
    <!-- form -->
    <form class="shadow-lg p-3 " v-if="seen">
      <div role="group">
        <label for="inputLive">Task:</label>
        <b-form-input id="inputLive" v-on:keypress="submit" v-model.trim="user.name" type="text" :state="nameState" aria-describedby="inputLiveHelp inputLiveFeedback" placeholder="Enter your name"></b-form-input>
        <b-form-invalid-feedback id="inputLiveFeedback">
          Name should be minimum of 3 character
        </b-form-invalid-feedback><br/>
      </div>
      <div>
        <label>Date:</label>
        <b-form-input type="date" v-model="user.date"></b-form-input><br/>
      </div>
      <div>
        <label>Time:</label>
        <b-form-input type="time" v-model="user.time"></b-form-input><br/>
      </div>
      <button type="cancel" class="btn" id="first">Cancel</button>
      <button type="button" class="btn btn-primary" id="second" v-on:click="submit">Submit</button>
    </form>
    <!-- from end -->
  
    <!-- table start -->
    <table class="table" striped hover :items="users" v-if="list">
      <thead class="thead-dark">
        <tr>
          <th scope="col">Status</th>
          <th scope="col">Task</th>
          <th scope="col">Date</th>
          <th scope="col">Time</th>
          <th scope="col" colspan="2">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id" id="list">
          <td>
            <div class="checkbox">
              <label><input type="checkbox" v-model="user.status"></label>
            </div>
          </td>
          <td> <span v-bind:class="{checked : user.status}">{{user.name}}</span></td>
          <td> <span>{{user.date}}</span> </td>
          <td> <span>{{user.time}}</span> </td>
          <td><a href="#" @click="deleteItem(user)" class="a">Delete</a>
            <a href="#" @click="edit(user)" v-b-modal.modalPrevent>Edit</a></td>
        </tr>
      </tbody>
    </table>
    <!-- table ends -->
  </div>
</template>

<script>
  import Form from "./Form";
  
  export default {
    name: "Todo",
    data() {
      return {
        message: "Welcome On TODO",
        seen: false,
        userCount: 0,
        list: false,
        users: [],
        user: {
          name: "",
          date: "",
          time: "",
          status:false
        },
        message : ''
      };
    },
    components: {
      Form,
    },
    computed: {
      nameState() {
        return this.user.name.length > 2 ? true : false;
      }
    },
    methods: {
      submit: function() {
        if (this.isEdit) {
          for (var i = 0; i < this.users.length; i++) {
            if (this.users[i].id == this.user["id"]) {
              this.users[i] = this.user;
              this.isEdit = false;
            }
          }
        } else {
  
          this.users.push({
            id: ++this.userCount,
            name: this.user.name,
            date: this.user.date,
            time: this.user.time,
          })
        }
        this.user = {
          name: "",
          date: "",
          time: "",
        }
        this.seen = false;
        this.message = "Task added to the list :)";
      },
      addform: function() {
        this.seen = true;
        this.list = false;
      },
      showlist: function() {
        this.seen = false;
        this.list = true;
      },
      deleteItem: function(user) {
        this.users.splice(this.users.indexOf(user), 1);
      },
      edit: function(user) {
        this.user = user;
        this.isEdit = true;
        this.seen = true;
        this.list = false;
      }
    }
  }
</script

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main {
    width: 50%;
    margin: 0 auto;
  }
  
  button {
    margin: 0 auto;
    margin-right: 50px;
  }
  
  a {
    color: #42b983;
  }
  
  label {
    float: left;
    font-size: 20px;
    font-weight: bold;
  }
  
  form {
    background: #F5F5F5;
    margin-top: 25px;
  }
  
  table {
    margin-top: 25px;
  }
  
  #first {
    margin-right: 15px;
  }
  
  .added {
    margin-top: 25px;
  }
  
  .a {
    margin-right: 15px;
  }
  
  .checkbox {
    margin-left: 35px;
  }
  
  .btn-toolbar {
    display: block;
  }
  
  .checked {
    text-decoration: line-through;
    color: #E6E6E6;
  }
</style>
