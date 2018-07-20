<template>
  <div class="testing">
    <p v-bind:submit-array="array"></p>
    <!-- <Form v-bind:edit-index="editIndex" v-bind:name="name" v-on:edit-item="edit" v-on:submit-item="submit" /> -->
    <ul>
        <li v-for="(item,index) in data" v-bind:key="index">
          <span>{{ item }}</span> 

          <a href="#" v-on:click.prevent="deleteItem(index)" >Delete</a>
          <a href="#" v-on:click.prevent="editItem(index)" >Edit</a>
        </li> 
      </ul>
      <p>{{list}}</p>
  </div>
</template>

<script>
import Vue from "vue";
import Form from "./Form";

export default {
  name: "List",
  components: {
    Form
  },
  data: function() {
    return {
      data: [],
      name: "",
      editIndex: -1
    };
  },
  methods: {
    array:function(ev){
console.log(ev);

},
    submit: function(name) {
      this.data.push(name);
      this.name = "";
    },
    edit: function(obj) {
      var { name, editIndex } = obj;
      Vue.set(this.data, editIndex, name);
      this.name = "";
      this.editIndex = -1;
    },
    deleteItem: function(index) {
      this.data.splice(index, 1);
    },
    editItem: function(index) {
      this.editIndex = index;
      this.name = this.data[index];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  /* display: inline-block; */
  margin: 0 10px;
}
ul li a {
  float: right;
  color: #42b983;
  margin-right: 15px;
}
ul li {
  border: 1px solid grey;
}
</style>
