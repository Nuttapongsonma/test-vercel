<script setup>
const route = useRoute()
const todoId = route.params.id

const BASE_URL = 'https://6805c80aca467c15be69e5d7.mockapi.io'

const { data: todo} = await useFetch(`${BASE_URL}/todos/${todoId}`)
</script>

<template>
    <div>
        {{ todoId }}
        {{ todo.name }}
    </div>
</template>