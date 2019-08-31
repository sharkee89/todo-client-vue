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
        flex-direction: column;
    }
    input[type="text"], input[type="date"] {
        padding: 5px;
        margin-bottom: 1em;
    }
    input[type="submit"] {
        background-color: palevioletred;
    }
</style>