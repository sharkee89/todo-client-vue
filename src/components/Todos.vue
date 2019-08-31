<template>
    <div class="todos">
        <input class="filter-val" type="text" v-model="search" placeholder="Filter todos by title">
        <div v-bind:key="todo._id" v-for="todo in filteredTodos">
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo._id)" v-on:update-todo="$emit('update-todo', todo)" />      
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: 'Todos',
    components: {
        TodoItem
    },
    data() {
        return {
            search: ''
        }
    },
    props: ['todos'],
    computed: {
        filteredTodos: function () {
            return this.todos.filter((todo) => {
                return todo.title.match(this.search);
            });
        }
    }
}
</script>

<style scoped>
    .todos {
        padding: 0 1.5em;
    }   
    .filter-val {
        width: 50%;
        padding: .5em;
        margin-top: 1em;
    }
</style>