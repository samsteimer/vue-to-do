<template>
    <div>
        <ul>
            <li v-for="todo in toDos" v-bind:key="todo.id">
                <span> <input type="checkbox" :checked="todo.done" @click="checkToDo(todo.id)"> {{ todo.todo }} Category: {{ todo.category }} <button @click="deleteToDo(todo.id)">Delete</button>
                </span>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['toDoDeleted', 'toDoChecked']);


const props = defineProps({
    toDos: {
        type: Array,
        required: true
    }
});

const deleteToDo = (id) => {
    emit('toDoDeleted', id);
};

const checkToDo = (id) => {
    emit('toDoChecked', id);
}

</script>