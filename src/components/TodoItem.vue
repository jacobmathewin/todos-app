<template>
    <div class="card-body">
        <p class="card-title" :class="todo.completed ? 'font-weight-light' : ''">{{todo.title}}</p>
        <button class="btn btn-sm" :class="todo.completed ? 'btn-light' : 'btn-outline-primary'" @click="$emit('mark-completed', todo.id)">
            <font-awesome-icon icon="check" />
        </button>
        <button class="btn btn-sm btn-outline-danger ml-1" @click="$emit('delete-todo-item', todo.id)">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',
    props: [
        'todo'
    ],
    methods: {
    }
}
</script>