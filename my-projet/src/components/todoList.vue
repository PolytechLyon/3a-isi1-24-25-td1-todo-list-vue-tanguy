<template>
    <div>
        <h2>Todo List</h2>
        <ol>
            <li v-for="(todo, index) in todos" :key="todo.id">
                <span>{{ todo.text }}</span>
                <button @click="deleteTodo(index)">Delete</button>
                <button @click="startEdit(index)">Edit</button>
            </li>
        </ol>
        
        <div v-if="editingIndex === null">
            <input v-model="newTodo" placeholder="Add a new task :" />
            <button @click="addTodo">Add</button>
        </div>

        <div v-if="editingIndex !== null">
            <input v-model="editTodo" />
            <button @click="confirmEdit">Confirm</button>
            <button @click="cancelEdit">Cancel</button>
        </div>
    </div>
</template>

  
<script>
export default {
    data() {
        return {
            todos: [],
            newTodo: '',
            editTodo: '',
            editingIndex: null,
        };
    },
    methods: {
        addTodo() {
            if (this.newTodo.trim()) {
                this.todos.push({ text: this.newTodo, id: Date.now() });
                this.newTodo = '';
            }
        },
        deleteTodo(index) {
            this.todos.splice(index, 1);
        },
        startEdit(index) {
            this.editingIndex = index;
            this.editTodo = this.todos[index].text;
        },
        confirmEdit() {
            if (this.editTodo.trim()) {
                this.todos[this.editingIndex].text = this.editTodo;
                this.editingIndex = null;
                this.editTodo = '';
            }
        },
        cancelEdit() {
            this.editingIndex = null;
            this.editTodo = '';
        },
    },
};
</script>

  