<template>
    <div class="notebook">
        <h1>Lista de Tarefas</h1>
        <div class="input-section">
            <label for="description">Descrição:</label>
            <input type="text" id="description" v-model="todo.description" />
            <label for="status">Status:</label>
            <select id="status" v-model="todo.status">
                    <option value="todo">A fazer</option>
                    <option value="doing">Fazendo</option>
                    <option value="done">Feito</option>
                </select>
        </div>
        <button @click="addTodo">Adicionar Tarefa</button>
        <hr>
        <div class="task-list">
            <div v-for="item in todoList" :key="item.id" v-bind:class="[item.status]">
                <span>{{ item.description }}</span>
                <select id="status" v-model="item.status">
                        <option value="todo">A fazer</option>
                        <option value="doing">Fazendo</option>
                        <option value="done">Feito</option>
                    </select>
                <button @click="removeTodo(item)">Excluir</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { reactive, ref } from 'vue';

//..define a reactive object
const todo = reactive({
    id: 0,
    description: '',
    status: 'todo',
});

//..define a reactive variable
const todoList = ref([
    { id: 1, description: 'Estudar vue.js', status: 'doing' },
    { id: 2, description: 'Estudar JavaScript', status: 'doing' },
    { id: 3, description: 'Lavar o carro', status: 'todo' },
    { id: 4, description: 'Entregar o TG', status: 'todo' },
]);

//.define a reactive variable to control the id increment
const lastId = ref(4);

const addTodo = () => {
    lastId.value++;
    todoList.value.push({
        id: lastId.value,
        description: todo.description,
        status: todo.status,
    });
    todo.id = 0;
    todo.description = '';
    todo.status = 'todo';
};

const removeTodo = (todo) => {
    let index = todoList.value.findIndex((item) => {
        return item.id == todo.id;
    });
    todoList.value.splice(index, 1);
};
</script>

<style scoped>
.notebook {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

h1 {
    font-size: 24px;
    text-align: center;
}

.input-section {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}

.input-section label {
    margin-right: 10px;
}

input[type="text"] {
    flex: 1;
    padding: 5px;
    border: none;
    border-bottom: 1px solid #ccc;
    font-size: 16px;
}

button {
    padding: 5px 10px;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

button:hover {
    background-color: #0056b3;
}

.task-list {
    margin-top: 20px;
}

.task-list>div {
    display: flex;
    align-items: center;
    padding: 10px;
    background-color: #f9f9f9;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-bottom: 10px;
}

.task-list>div span {
    flex: 1;
}

.task-list>div select {
    margin-right: 10px;
}

.todo {
    background-color: #ffe3e3;
    border-color: #ffacac;
}

.doing {
    background-color: #d5ffd5;
    border-color: #9dff9d;
}

.done {
    background-color: #e2f3ff;
    border-color: #aad7ff;
}
</style>