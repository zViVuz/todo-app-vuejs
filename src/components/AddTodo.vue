<template>
    <div class="tools">
        <form class="left" @submit="addTodo">
            <input type="text" placeholder="Fill the blank" v-model="title" />
            <input type="submit" value="Add" class="btn-add" />
        </form>
        <!-- <button class="right" @click="hideCompleted = !hideCompleted">
            {{ hideCompleted ? 'Show all' : 'Hide completed' }}
        </button> -->
    </div>
</template>

<script>
import { ref, toRefs, computed } from 'vue'
export default {
    name: 'AddTodo',
    props: ['nextId', 'todos'],
    setup(props, context) {
        const { nextId, todos } = toRefs(props) // Sử dụng toRefs để truy cập giá trị props
        const hideCompleted = ref(false)
        const filterTodo = () => {
            context.emit('filter-todo', hideCompleted.value
                ? todos.value.filter((t) => !t.checked)
                : todos.value)
        }

        const title = ref('')
        const addTodo = (event) => {
            event.preventDefault();

            const newTodo = {
                id: nextId.value, // Sử dụng nextId được truyền từ props
                title: title.value,
                checked: false,
                date: new Date().toLocaleDateString()
            }
            context.emit('add-todo', newTodo)

            title.value = ''
        }
        return {
            title,
            addTodo,
            filterTodo
        }
    }
}
</script>

<style>
.tools {
    display: flex;
}

.tools .right {
    flex: 2;
}

.tools .left {
    flex: 10;
    display: flex;
}

.left input[type='text'] {
    flex: 10;
    padding: 5px;
}

.left input[type='submit'] {
    flex: 2
}
</style>
