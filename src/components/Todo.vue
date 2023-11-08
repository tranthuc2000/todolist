<script setup>
import { ref } from 'vue';
import TodoMain from './TodoMain.vue'
import NewFile from './NewFile.vue'
const isCreate = ref(false)

const todoContent = ref([
    {
        id: 1,
        title: "Todo1",
        content: "LLorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum",
        isDone: false
    },
    {
        id: 2,
        title: "Todo2",
        content: "Làm cái gì đó",
        isDone: false
    },
    {
        id: 3,
        title: "Todo3",
        content: "Làm cái gì đó",
        isDone: true
    }
])
const handleUpdate = (value) => {
    todoContent.value.forEach(element => {

        if (element.id == value.id) {
            element.isDone = value.isDone
        }
    });
}
const handleDelete = (value) => {
    todoContent.value = todoContent.value.filter(val => val.id !== value)
}
const handleUpdateTodo = (val) => {
    const idlast = todoContent.value[todoContent.value.length - 1].id + 1
    todoContent.value.push({
        id: idlast,
        title: val.title,
        content: val.content,
        isDone: false
    })
}
const handleEditTask = (value) => {
    console.log(value)
    todoContent.value.forEach((val) => {
        if(value.id === val.id){
            val.content = value.content
            val.title = value.title
        }
    }
    )
}
</script>
<template>
    <div class="container">
        <div class="header">
            <span class="project" @click="isCreate = false" :class="{ 'active': !isCreate }">Project</span>
            <span class="add" @click="isCreate = true" :class="{ 'active': isCreate }">Add New Project</span>
        </div>
        <div v-if="!isCreate">
            <TodoMain :content="todoContent" @updateIsDone="handleUpdate" @delete="handleDelete" @editTask="handleEditTask"/>
        </div>

        <div v-if="isCreate">
            <NewFile @update="handleUpdateTodo"  />
        </div>
    </div>
</template>

    
<style scoped>
.active {
    text-decoration: underline;
    color: blueviolet;
}

.container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
   
    margin: auto;
}

.header {
    font-size: x-large;
    text-align: center;
    color: black
}

.project {

    padding: 0px 10px;
    border-right: 3px solid black;
}

.add {
    padding: 0px 10px;

}
</style>