<template>
    <div class="d-flex flex-row flex-wrap justify-content-center">
        <div class="card m-2 col-xl-3 col-lg-4 col-sm-5 col-xs-12" :key="todo.id" v-for="todo in todos">
            <TodoItem :todo="todo" 
                @mark-completed="$emit('mark-completed', todo.id)" 
                @delete-todo-item="$emit('delete-todo-item', todo.id)" />
        </div>
    </div>    
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
    name: "Todos",
    props: [
        "todos"
    ],
    components: {
        TodoItem
    },
    methods: {
    }
}
</script>

<style scoped>

</style>