<script setup> 
import { ref } from "vue";
// 1 Vise en liste af opgaver (dummydata)
const tasks = ref([
    {id: 1, text: 'Kram en lampe'},
    {id: 2, text: 'Fjern nullermænd fra navlen'},
    {id: 3, text: 'Lugt til din albue'},
    {id: 4, text: 'Hvisk til en plante'},
    {id: 5, text: 'Giv high-five til en væg'},
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
    {{ editTask }}
    <div class="todo-app">
        <h2>Opgaveliste</h2>
        <!-- imput + knap til at tilføje  -->
        <input v-model="newTask" placeholder="Tilføj en ny opgave" />
        <button @click="addTask" :disabled="newTask.trim() ===''">Tilføj</button>
        <!-- Ny knap til at redigere -->
        <button @click="editTask = !editTask">
    {{ editTask ? 'Gem' : 'Rediger' }}
    </button>
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
    background: linear-gradient(135deg, deeppink, hotpink);
    color: #33041D;
    border-radius: 15px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);

    h2 {
        margin-bottom: 30px;
        font-size: 4rem;
        text-align: center;
        text-transform: uppercase;
        width: 100%;
        font-weight: bold;
        letter-spacing: 2px;
        color: #fff;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }

    input {
    padding: 12px;
    margin-right: 10px;
    border: 2px solid #000000;
    border-radius: 8px;
    font-size: 1rem;
    width: 60%;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;

    &:focus {
        border-color: #FF1493;
        outline: none;
        box-shadow: 0 0 8px rgba(255, 20, 147, 0.6);
    }

    &::placeholder {
        color: #D3D3D3; /* Lighter placeholder color */
        font-style: italic;
    }
}

    button {
        padding: 12px 24px;
        background-color: rgba(0, 0, 0, 0.8);
        color: #FF1493;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        font-size: 1rem;
        font-weight: bold;
        transition: background-color 0.3s ease, transform 0.2s ease;

        &:hover:not(:disabled) {
            background-color: rgba(0, 0, 0, 1);
            transform: scale(1.05);
        }

        &:active:not(:disabled) {
            transform: scale(0.95);
        }

        &:disabled {
            background-color: #ccc;
            cursor: not-allowed;
            color: #888;
        }
    }

    ul {
        list-style-type: none;
        padding: 0;
        margin-top: 30px;

li {
    padding: 15px;
    margin: 10px 0;
    background-color: rgba(0, 0, 0, 0.8);
    color: #FF1493;
    border: 2px solid #000000;
    border-radius: 8px;
    font-weight: 500;
    font-size: 1.1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.2s ease;

    &:hover {
        background-color: rgba(0, 0, 0, 0.9);
        transform: translateX(5px);
        box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
    }
}
    }

    p {
        color: #fff;
        font-size: 1.2rem;
        margin-top: 20px;
    }
}
</style>