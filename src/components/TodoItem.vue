<template>
    <p :class="['todo-item', todoProps.checked ? 'btn-checked' : '']">
        <input type="checkbox" :checked="todoProps.checked" @change="markItemChecked">
        {{ todoProps.title }}
        <button class="del-btn" v-on:click="deleteItem">X</button>
    </p>
</template>

<script>
import { ref } from 'vue'
export default {
    name: 'TodoItem',
    props: ['todoProps'],
    setup(props, context) {
        const markItemChecked = () => {
            context.emit('item-checked', props.todoProps.id)
        }
        const deleteItem = () => {
            context.emit('delete-item', props.todoProps.id)
        }
        return {
            markItemChecked,
            deleteItem
        }
    }
}
</script>

<style>
.todo-item {
    background: whitesmoke;
    padding: 10px;
    margin: 0px;
    border-bottom: 1px solid #ccc dotted;
}

.btn-checked {
    text-decoration: line-through;
}

.del-btn {
    cursor: pointer;
    background: skyblue;
    color: white;
    border: 1px;
    float: right;
}
</style>