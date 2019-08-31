<template>
    <div class="todo-item">
        <div>
            <p>{{todo.title}}</p>
            <p>{{todo.description}}</p>
            <p>{{todo.date | formatDate}}</p>
            <button v-on:click="toggleEdit" class="edit-btn">Edit</button>
            <button @click="$emit('del-todo', todo._id)" class="del">x</button>
        </div>
        <EditTodo v-show="isEditMode" v-bind:todo="todo" v-on:update-todo="$emit('update-todo', todo)" v-on:clear-edit="clearEdit"></EditTodo>
    </div>
</template>
<script>
import EditTodo from './EditTodo';
export default {
    name: 'TodoItem',
    data() {
        return {
            isEditMode: false
        }
    },
    components: {
        EditTodo
    },
    props: ['todo'],
    methods: {
        toggleEdit() {
            this.isEditMode = !this.isEditMode;
        },
        clearEdit() {
            this.isEditMode = false;
        }
    }
}
</script>
<style scoped>
    .todo-item {
        background: transparent;
        padding: 10px;
        border: 1px lightgray dotted;
        position: relative;
        margin: 1em 0;
        border-radius: 10px;
        box-shadow: 5px 5px lightgray;
    }
    .del {
        position: absolute;
        top: 15%;
        right: 1%;
        background: palevioletred;
        color: #fff;
        padding: 5px 9px;
        border-radius: 50%;
        cursor: pointer;
        float: right;
    }
    .edit-btn {
        background-color: palevioletred;
        padding: 1em 3em;
        border: none;
        color: #fff;
        margin-bottom: 1em;
    }
</style>