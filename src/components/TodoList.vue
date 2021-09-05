<template>
  <div class="todo-list">
      <form class="ui form">
            <div class="fields">
                <div class="ten wide field">
                    <input class="six wide field" type="text" v-model="search" placeholder="Search" />
                </div>
            </div>
      </form>
    <div class="data">
      <table class="ui celled table">
        <thead>
          <tr>
            <th>Title</th>
            <th>Description</th>
            <th>Due Date</th>
            <th style="width: 148px;">Action</th>
          </tr>
        </thead>

        <tbody>
            <list
             v-for="list in filteredList"
             :key="list.id"
             :list="list"
             @onDelete="onDelete"
             @onEdit="onEdit" />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import List from './List.vue'

export default {
    name: 'TodoList',
    components: {
        List
    },

    data() {
        return {
            search: '',
        }
    },

    props: {
        lists: {
            type: Array
        }
    },

    methods: {
        onDelete(id) {
            // window.console.log('customer list deleted', id);
            this.$emit('onDelete', id);
        },

        onEdit(data) {
            this.$emit('onEdit', data);
        }
    },

    computed: {
        filteredList() {
        return this.lists.filter(post => {
            return post.title.toLowerCase().includes(this.search.toLowerCase());
         });
        }
    }
}
</script>

<style></style>
