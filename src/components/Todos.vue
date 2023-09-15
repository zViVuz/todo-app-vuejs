<template>
    <AddTodo @add-todo="addTodo" @filter-todos="filterTodos" :nextId="nextId" :todos="todos" />
    <TodoItem v-for="todo in todos" v-bind:key="todo.id" v-bind:todoProps="todo" v-on:item-checked="markItemChecked"
        @delete-item="deteleTodo" v-bind:todos="todos" />
</template>

<script>
import { ref, computed } from 'vue'
import TodoItem from './TodoItem.vue'
import AddTodo from './AddTodo.vue'
export default {
    name: 'Todos',
    components: { TodoItem, AddTodo },
    setup() {

        const todos = ref([
            {
                id: 1,
                title: 'Task 1',
                checked: false,
                date: '1/15/2023'
            },
            {
                id: 2,
                title: 'Task 2',
                checked: false,
                date: '9/23/2023'
            },
            {
                id: 3,
                title: 'Task 3',
                checked: false,
                date: '9/15/2013'
            }
        ])
        const markItemChecked = id => {
            todos.value = todos.value.map(todo => {
                if (todo.id === id) todo.checked = !todo.checked
                return todo
            })
        }
        const deteleTodo = id => {
            todos.value = todos.value.filter(todo => todo.id !== id)
        }

        const addTodo = newTodo => {
            newTodo.id = nextId.value++
            todos.value.push(newTodo)
        }
        const nextId = ref(todos.value.length + 1)

        const filterTodos = filteredList => {
            todos.value = filteredList
        }
        const reversedTodo = computed(() => {
            return todos.value.slice().reverse()
        })
        return {
            todos,
            markItemChecked,
            deteleTodo,
            addTodo,
            nextId,
            filterTodos,
            reversedTodo
        }
    }
}
</script>

<style></style>