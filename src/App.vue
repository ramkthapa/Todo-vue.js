<template>
  <div id="app">
    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <span href="#" class="header item">Todo App with Vue.js</span>
      </div>
    </div>

    <div class="ui main container">
      <app-form :form="form" @onFormSubmit="onFormSubmit" />
      <loader v-if="loader" />
      <todo-list 
        :lists = 'lists' 
        @onDelete = "onDelete"
        @onEdit = "onEdit"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import TodoList from './components/TodoList.vue';
import Loader from './components/Loader.vue';
import AppForm from './components/AppForm.vue';


  export default {
    name: 'App',
    components: {
        AppForm,
        TodoList,
        Loader
    },

    data() {
      return {
        url: 'http://localhost:3000',
        lists: [],
        form: {title: '', description: '', dueDate: ''},
        loader: false
      };
    },

    methods: {
      getLists() {
        this.loader = true;
        axios.get(`${this.url}/read`).then(response => {
          this.lists = response.data;
          this.loader = false;
        });
      },

      onFormSubmit(data) {
          if(data._id) {
            console.log('Edited.....');
              this.editList(data);
          } else {
            console.log('create.....');
              this.createList(data);
          }
          
      },

      createList(data) {

        this.loader = true;
        axios.post(`${this.url}/create`, {
          title: data.title,
          description: data.description,
          dueDate: data.dueDate
        }).then(() => {
            this.getLists();
        }).catch(err => {
          console.log(err);
        });
      },


      editList(data) {

        this.loader = true;

        axios.put(`${this.url}/update`, {
          title: data.title,
          description: data.description,
          dueDate: data.dueDate,
          _id: data._id
        }).then(() => {
          this.getLists();
        }).catch(err => {
          console.log(err);
        });
      },

      deleteList(id) {
        console.log('Just Clicked delete');
        this.loader = true;
        axios.delete(`${this.url}/delete/${id}`)
          .then(() => {
            this.getLists();
          })
          .catch(err => {
            console.log(err);
          });
      },

      onEdit(data) {
        this.form = data;
      },

      onDelete(id) {
        this.deleteList(id);
      },

    },

    created() {
      this.getLists();
    }

  }

</script>

<style scoped></style>
