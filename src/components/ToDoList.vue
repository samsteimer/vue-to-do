<template>
    <div class="conatainer mb-1">
        <ul class="list-group">
            <li class="list-group-item d-flex justify-content-between align-itmes-center" v-for="todo in toDos" v-bind:key="todo.id">
                <div class="mt-1">
                    <input class="form-check-input " type="radio" :checked="todo.done" @click="checkToDo(todo.id)">
                    <label class="form-check-label ms-2"> {{ todo.todo }} </label>
                </div>
                <div class="d-flex align-items-start">
                    <span class="me-2 mt-1"> {{ todo.category }} </span>
                    <button @click="deleteToDo(todo.id)" class="btn btn-danger btn-sm">Delete</button>
                </div>
                 
                    
                
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
<style scoped>
.category-container {
    width: 10px;
}

</style>