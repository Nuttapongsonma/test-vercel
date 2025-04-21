<script setup>
const BASE_URL = 'https://6805c80aca467c15be69e5d7.mockapi.io'

const todos = ref([])
const todoText = ref('')

const LoadTodo = async () =>{
    const {data} = await useFetch(`${BASE_URL}/todos`)
    todos.value = data.value
}

const addTodo = async () => {
    try{
        await useFecth(`${BASE_URL}/todos`, {
        method: 'POST',
        body: {
            name: todoText.value,
            status: 'Pending'
        }
    })
    await LoadTodo()
    } catch (error) {
        console.log('Error adding todo:', error)
    }
}

const editTodo = async (todoID, todoData) => {
    try{
        await useFetch(`${BASE_URL}/todos/${todoID}`, {
            method: 'PUT',
            body: {
                status: todoData.status,
            }
        })
        await LoadTodo()
    } catch (error) {
        console.log('Error editing todo:', error)
    }
}

LoadTodo()
</script>

<template>
    <div>
        <!-- {{ todoText }} -->
        <input v-model="todoText" type="text">
        <button @click="addTodo">Add</button>
    </div>

    <ul>
        <li v-for="todo in todos">
            {{ todo.id }}
            {{ todo.name }}
            <!-- {{ todo.status }} -->
            <select v-model="todo.status">
                <option>North</option>
                <option>East</option>
                <option>South</option>
                <option>West</option>
            </select>
            <button @click="editTodo(todo.id, todo)">Update</button>
            <NuxtLink :to="`/todos/${todo.id}`">Edit</NuxtLink>
        </li>
    </ul>
</template>