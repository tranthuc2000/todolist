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
        if (value.id === val.id) {
            val.content = value.content
            val.title = value.title
        }
    }
    )
}
</script>
<template>
    <div class=" flex justify-center items-center ">
        <div class=" flex justify-center p-4">
            <span class="border-r-4 border-gray-800 pr-4 text-xl " @click="isCreate = false"
                :class="{ 'active': !isCreate }">Project</span>
            <span class=" pl-4 text-xl " @click="isCreate = true" :class="{ 'active': isCreate }">Add New Project</span>
        </div>
    </div>
    <div v-if="!isCreate" class="flex justify-center ">
        <TodoMain :content="todoContent" @updateIsDone="handleUpdate" @delete="handleDelete" @editTask="handleEditTask" />
    </div>

    <div v-if="isCreate" class="flex justify-center ">
        <NewFile @update="handleUpdateTodo" />
    </div>
</template>

    