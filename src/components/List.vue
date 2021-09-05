<template>
    <tr>
        <td>{{ list.title }}</td>
        <td>{{ list.description }}</td>
        <td>{{ list.dueDate }}</td>
        <td>
            <button class="mini ui blue button" @click="onEdit">Edit</button>
            <button class="mini ui red button" @click="onDelete">Delete</button>
        </td>
    </tr>
</template>

<script>

export default {
    name: 'List',
    props: {
        list: {
            type: Object
        }
    },
    methods: {
        onDelete() {
            this.$emit('onDelete', this.list._id);
        },

        onEdit() {
            this.$emit('onEdit', this.list);
        }
    }
}
</script>

<style scoped></style>
