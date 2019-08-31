<template>
    <div>
        <form @submit="updateTodo">
            <input type="text" v-model="todo.title" name="title" placeholder="Enter title...">
            <input type="text" v-model="todo.description" name="description" placeholder="Enter description...">
            <input type="date" v-model="todo.date" name="date" placeholder="Enter date...">
            <input type="submit" value="Update" class="btn">
        </form>
    </div>
</template>
<script>
export default {
    name: 'EditTodo',
    props: ['todo'],
    methods: {
        updateTodo(e) {
            e.preventDefault();
            this.$emit('update-todo', this.todo);
            this.$emit('clear-edit');
        }
    }
}
</script>
<style scoped>
    form {
        display: flex;
    }
    input[type="text"] {
        flex: 1;
        padding: 5px;
    }
    input[type="date"] {
        flex: 1;
        padding: 5px;
    }
    input[type="submit"] {
        flex: 2;
        background-color: palevioletred;
    }
</style>