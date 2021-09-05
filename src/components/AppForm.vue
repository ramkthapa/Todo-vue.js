<template>
   <div class="todo-form">
       <form id="todoForm" class="ui form">
           <div class="fields">
           <div class="four wide field">
                <label for="email">Title:</label>
                <input 
                    type="text" 
                    name="title"
                    @change="handleChange"
                    :value="form.title" />    
           </div>
            <div class="six wide field">
                <label for="description">Description:</label>
                <input 
                    type="text" 
                    name="description"
                    @change="handleChange"
                    :value="form.description" />
            </div>
            <div class="four wide field">   
                <label class="datepicker-label" for="dueDate">Due Date:</label>
                <input 
                    type="date" 
                    name="dueDate" 
                    @change="handleChange"
                    :value="form.dueDate" /> 
            </div>
            <div class="two wide field ">
                <button class="ui primary button submit-button" type="submit" @click="onFormSubmit">Add todo list</button>
            </div>
            </div>
        </form>
    </div>
</template>

<script>
// import Datepicker from 'vuejs-datepicker';

export default {
    name: 'AppForm',
    components: {
        // Datepicker
  },

  props: {
      form: {
          type: Object
      }
  },

  methods: {

        handleChange(event) {
            const { name, value } = event.target;
            let form = this.form;
            form[name] = value;
            this.form = form;
        },

      onFormSubmit(event) {

        event.preventDefault();

        if(this.formValidation()) {
            this.$emit('onFormSubmit', this.form);

            //clear form
            this.clearFormFields();
        }

      },

      formValidation() {
          if(document.getElementsByName('title')[0].value === '') {
              alert('Enter title');
              return false;
          }
          if(document.getElementsByName('description')[0].value === '') {
              alert('Enter description');
              return false;
          }
          if(document.getElementsByName('dueDate')[0].value === '') {
              alert('Enter due date');
              return false;
          }

          return true;
        },

        clearFormFields() {
            document.getElementById("todoForm").reset();
        }
   },
}
</script>

<style>
.submit-button {
    margin-top: 25px !important;
}
.todo-form {
    margin: 60px 0 0 !important;
}
</style>
