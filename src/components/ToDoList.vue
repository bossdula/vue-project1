<script setup>
import { ref } from "vue";

const newTask =ref('');
const tasks = ref([]);

const addTask = () => {
    if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = "";
    }
}

const removeTask = (index) => {
    tasks.value.splice(index, 1);
}
</script>



<template>
    <div class="todo-app">
        <div class="task-input">
            <input v-model="newTask" @keyup:enter="addTask" placeholder="Add new task">
            <button @click="addTask">Add to do</button>
        </div>

        <ul class="task-list">
            <li v-for="(task, index) in tasks" :key="index" class="task-item">
                {{ task }}
                <button @click="removeTask(index)" class="remove-button">Remove</button>
            </li>
        </ul>
    </div>
</template>


<style scoped>
.todo-app {
    max-width: 400px;
    margin: 40px auto;
    padding: 20px;
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}

.task-input {
    align-items: center;
    padding: 20px;
    border-bottom: 1px solid #ccc;
}

input {
    width: 80%;
    padding: 10px;
    font-size: 16px;
    border: none;
    border-radius: 5px;
    margin-bottom: 10px;
}

.task-input button {
    padding: 10px;
    font-size: 16px;
    background-color: #4CAF50;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.class-list {
    padding: 20px;
    display: inline;
}

ul {
    list-style: none;
}
ul li {
    padding: 10px;
    border-bottom: 1px solid #ccc;
    text-transform: uppercase;
}
.remove-button {
    float: right;
    padding: 5px;
    font-size: 16px;
    background-color: #e21919;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}
</style>