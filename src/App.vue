<template>
    <div id="app" class="">
        <Header 
            @search-item="searchItem"
            @reset-search="resetSearch" />
        <Todos v-bind:todos=todos 
            @mark-completed="markCompleted"
            @delete-todo-item="deleteTodoItem" />
        <LoadingCurtain v-show="showLoading" />
    </div>
</template>

<script>

import Header from './components/Header'
import Todos from './components/Todos'
import LoadingCurtain from './components/LoadingCurtain'
import axios from 'axios'

export default {
    name: 'App',
    components: {
        Header,
        Todos, 
        LoadingCurtain
    },
    data() {
        return {
            todos: [],
            todosBackup: [],
            showLoading: false
        }
    },
    created() {
        this.loadTodos();
    },
    methods: {
        markCompleted(id) {
            console.log(`Mark as completed: ${id}`);
            this.showLoading = true;
            let todoObj = this.todos.filter(todo => todo.id === id);
            todoObj = todoObj[0];

            // Toggle completed
            if(todoObj.completed)
                todoObj.completed = false;
            else
                todoObj.completed = true;

            fetch('https://jsonplaceholder.typicode.com/todos/'+id, {
                method: 'PUT',
                body: JSON.stringify(todoObj),
                headers: {
                    "Content-type": "application/json; charset=UTF-8"
                }
            })
            .then(response => response.json())
            .then(json => {
                console.log(json);
                // this.loadTodos();
                this.showLoading = false;
            })
        }, 
        loadTodos() {
            this.showLoading = true;
            axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
                .then(res => {
                    this.todos = res.data;
                    this.showLoading = false;
                })
                .catch(err => console.log(err));
        }, 
        deleteTodoItem(id) {
            this.showLoading = true;
            fetch('https://jsonplaceholder.typicode.com/todos/'+id, {
                method: 'DELETE',
            })
            .then(()=>{
                // this.loadTodos();
                this.todos = this.todos.filter(todo => todo.id !== id);
                this.showLoading = false;
            });
        }, 
        searchItem(text) {
            if(this.todosBackup.length===0)
                this.todosBackup = this.todos;

            this.todos = this.todosBackup;
            this.todos = this.todos.filter(todo => todo.title.search(text)!==-1)
        },
        resetSearch() {
            this.todos = this.todosBackup;
        }
  }
}
</script>

<style>

</style>
