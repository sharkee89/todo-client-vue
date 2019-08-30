<template>
    <div class="todo-item">
        <p>
            <p>{{todo.title}}</p>
            <p>{{todo.description}}</p>
            <p>{{todo.date | formatDate}}</p>
            <button @click="$emit('del-todo', todo._id)" class="del">x</button>
        </p>
    </div>
</template>
<script>
export default {
    name: 'TodoItem',
    props: ['todo']
}
</script>
<style scoped>
    .todo-item {
        background: transparent;
        padding: 10px;
        border: 1px green dotted;
        position: relative;
        margin: 1em 0;
        border-radius: 10px;
        box-shadow: 5px 5px forestgreen;
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
</style>