<script setup> 
import { ref } from "vue";
// 1 Vise en liste af opgaver (dummydata)
const tasks = ref([
    {id: 1, text: 'Handle'},
    {id: 2, text: 'Vaske tøj'},
    {id: 3, text: 'Gøre rent'},
    {id: 4, text: 'Vande planter'},
    {id: 5, text: 'Skift sengetøj'},
]);
// 2 Oprette en ny opgave
const newTask = ref("");

// Rediger opgaver
const editTask = ref(false) 

// tilføj ny opgave til listen
const addTask=() =>{
    if (newTask.value.trim()!="") { //removes whitespace
        tasks.value.push({ // add element to array
            id: tasks.value.length + 1, //id genator
            text: newTask.value // retrieves the current value of an input field in a form
        });
        newTask.value = ""; //Nulstiller inputfeltet
        
    }
};

    // Slet opgaver
    const deleteTask = (taskId) =>{
        tasks.value = tasks.value.filter((task) => task.id !== taskId);
    }


</script>

<template>
    <div class="todo-app">
        <h2>Opgaveliste</h2>
        <!-- imput + knap til at tilføje  -->
<div class="cta_knapper">
    <input v-model="newTask" placeholder="Tilføj en ny opgave" />
        <button @click="addTask" v-bind-disabled="newTask.trim() ==''">Tilføj</button>
        <!-- Ny knap til at redigere -->
        <button @click="editTask = !editTask">
    {{ editTask ? 'Gem' : 'Rediger' }}
    </button>
</div>


<!-- Ny knap til at slette  -->

    <!-- Listen vises hvis der er opgaver -->
    <ul v-if="tasks.length > 0">
    
    <li v-for="task in tasks" :key="task.id" :contenteditable="editTask">
        {{ task.text }}
        <button @click="deleteTask(task.id)" v-show="editTask">❌ Slet</button>
    </li>
   </ul>
   <p v-else>Ingen opgaver tilføjet endnu!</p>
    </div>


</template>

<style scoped lang="scss">
.todo-app {
    max-width: 700px;
    margin: 0 auto;
    padding: 40px;
    text-align: center;
    background: linear-gradient(135deg, #2e2e2e, #4b5563); 
    color: #e5e7eb;
    border-radius: 15px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);

    h2 {
        margin-bottom: 30px;
        font-size: 4rem;
        text-align: center;
        text-transform: uppercase;
        width: 100%;
        font-weight: bold;
        letter-spacing: 2px;
        color: #f9fafb; 
        text-shadow: 2px 2px 6px rgba(0, 0, 0, 0.5);
    }

    .cta_knapper {
        display: flex;
        gap: 10px;
        justify-content: center;
    }

    input {
        padding: 12px;
        margin-right: 10px;
        border: 2px solid #9ca3af; 
        border-radius: 8px;
        font-size: 1rem;
        width: 60%;
        background-color: #f3f4f6; 
        color: #111827;
        transition: border-color 0.3s ease, box-shadow 0.3s ease;

        &:focus {
            border-color: #3b82f6; 
            outline: none;
            box-shadow: 0 0 8px rgba(59, 130, 246, 0.4);
        }

        &::placeholder {
            color: #9ca3af;
            font-style: italic;
        }
    }

    button {
        padding: 12px 24px;
        background-color: #1f2937; 
        color: #f9fafb; 
        border: none;
        border-radius: 8px;
        cursor: pointer;
        font-size: 1rem;
        font-weight: bold;
        transition: background-color 0.3s ease, transform 0.2s ease;

        &:hover:not(:disabled) {
            background-color: #374151;
            transform: scale(1.05);
        }

        &:active:not(:disabled) {
            transform: scale(0.95);
        }

        &:disabled {
            background-color: #6b7280;
            cursor: not-allowed;
            color: #d1d5db;
        }
    }

    ul {
        list-style-type: none;
        padding: 0;
        margin-top: 30px;

        li {
            padding: 15px;
            margin: 10px 0;
            background-color: #111827;
            color: #f9fafb;
            border: 1px solid #4b5563;
            border-radius: 8px;
            font-weight: 500;
            font-size: 1.1rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.2s ease;

            &:hover {
                background-color: #1f2937;
                transform: translateX(5px);
                box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            }
        }
    }

    p {
        color: #e5e7eb;
        font-size: 1.2rem;
        margin-top: 20px;
    }
}

</style>