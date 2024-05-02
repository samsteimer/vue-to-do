<template>
    <div>
        <form @submit.prevent="onSubmit">
            <div>
                <label for="todo">To Do</label>
                <input type="text" id="todo" v-model="todo">
            </div>
            <div>
                <label for="category">Category</label>
                <input type="text" id="category" v-model="category">
            </div>
            <div>
                <button>Add To Do</button>
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