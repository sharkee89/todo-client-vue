<template>
    <div class="adt">
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="Enter title...">
            <input type="text" v-model="description" name="description" placeholder="Enter description...">
            <input type="date" v-model="date" name="date" placeholder="Enter date...">
            <input type="submit" value="Add todo" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: 'AddTodo',
    data() {
        return {
            title: '',
            description: '',
            date: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                title: this.title,
                description: this.description,
                date: this.date
            }
            this.$emit('add-todo', newTodo);
            this.title = '';
            this.description = '';
            this.date = '';
        }
    }
}
</script>

<style scoped>
    .adt {
        margin-top: 1.5em;
        padding: 0 1.5em;
    }   
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