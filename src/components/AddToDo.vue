<template>
    <div class="container rounded border">
        <form @submit.prevent="onSubmit">
            <div class="form-group">
                <label for="todo">To Do</label>
                <input type="text" id="todo" class="form-control" v-model="todo">
            </div>
            <div class="form-group mb-2">
                <label for="category">Category</label>
                <input type="text" id="category" class="form-control" v-model="category">
            </div>
            <div class="form-group mb-2">
                <button type="submit" class="btn btn-outline-primary">Add To Do</button>
            </div>
        </form>
    </div>
        
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const todo = ref('');
const category = ref('');

const emit = defineEmits(['toDoSubmitted']);

const onSubmit = () => {
    if(!todo.value || !category.value) {
        alert.error('Must enter To Do an Category');
        return;
    }

    const toDoData = {
        todo: todo.value,
        category: category.value
    }
    
    emit('toDoSubmitted', toDoData);

    todo.value = '';
    category.value = '';
}


</script>