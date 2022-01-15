<template>
    <div class="w-full md:w-1/2 mx-auto h-100 p-2 text-center">
        <form class="flex justify-around" @submit.prevent="addTodo">
            <input
                v-model="todo"
                name="todo"
                id="todo"
                class="w-5/6 px-2 text-sm text-gray-700 placeholder-gray-600 border rounded-lg focus:outline-none focus:ring focus:border-indigo-400"
                type="text"
                placeholder="Ingrese una tarea..."
                maxlength="60"
            />
            <button
                class="w-8 h-8 md:w-10 md:h-10 text-white rounded-full shadow-lg inline-flex items-center justify-center justify-self-end focus:outline-none focus:ring bg-indigo-600 hover:bg-indigo-500 active:bg-indigo-700"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-6 w-6"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                >
                    <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M12 4v16m8-8H4"
                    />
                </svg>
            </button>
        </form>
        <button
            class="block mx-auto w-1/2 my-2 focus:outline-none focus:ring bg-gray-400 hover:bg-gray-500 active:bg-gray-700 text-white rounded shadow"
            @click="removeAll"
        >Limpiar lista</button>
        <button
            class="block mx-auto w-1/2 my-2 focus:outline-none focus:ring bg-gray-400 hover:bg-gray-500 active:bg-gray-700 text-white rounded shadow"
            @click="removeCompleted"
        >Limpiar completados</button>
        <ul class="mt-2 h-full text-left">
            <li
                :class="todo.done ? 'bg-green-400 text-white' : 'bg-white'"
                class="flex justify-around shadow-lg rounded-md mb-2 h-auto"
                v-for="(todo,index) in todos"
                :key="todo.id"
            >
                <span
                    @click="todo.done = !todo.done"
                    class="w-5/6 pl-3 break-words"
                >{{ todo.content }}</span>
                <button @click="removeTodo(index)" class="inline-flex justify-center items-center">
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-5 w-5"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                    >
                        <path
                            fill-rule="evenodd"
                            d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                            clip-rule="evenodd"
                        />
                    </svg>
                </button>
            </li>
        </ul>
    </div>
</template>

<script setup>
import { v4 as uuidv4 } from 'uuid';
import { ref } from "vue"


const todo = ref('')
const todos = ref([])

function addTodo() {
    if (todo.value !== '') {
        todos.value.push({
            id: uuidv4(),
            done: false,
            content: todo.value,
        })
        todo.value = '';
    }
}

function removeTodo(index) {
    todos.value.splice(index, 1)
}

function removeAll() {
    todos.value = []
}

function removeCompleted() {
    todos.value = todos.value.filter(todo => !todo.done)
}

</script>