<script setup>
import { ref } from 'vue';
import TodoItem from './TodoItem.vue';
import NewFile from './NewFile.vue';

const props = defineProps(['content'])
const emit = defineEmits(['updateIsDone', 'delete','editTask'])
const link = ref('all')
const inputValue = ref('')
const textValue = ref('')
const isEdit = ref(false)
const id = ref(0)
const title = ref({
    all: "ALL PROJECT ",
    complete: "COMPLETED PROJECT",
    ongoing: "ONGOING PROJECT"
})

const handleIsDone = (value) => {
    emit('updateIsDone', value)
}

const handleDel = (value) => {
    emit('delete', value)
}

const handleEdit= (value) => {
    isEdit.value =true
    id.value =value.id
    inputValue.value = value.title
    textValue.value = value.content
    
}   

const handleReset = (value) => {
    
    emit('editTask',value)
    isEdit.value = !isEdit.value

}
</script>
<template>
    <div class="all">
        <div class="container" v-show="!isEdit">
            <div class="title" @click="link = 'all'" :class="{ 'active': link === 'all' }">{{ title.all }}</div>
            <div class="title" @click="link = 'completed'" :class="{ 'active': link === 'completed' }">{{ title.complete }}</div>
            <div class="title" @click="link = 'ongoing'" :class="{ 'active': link === 'ongoing' }">{{ title.ongoing }}</div>
        </div>
        <div v-if = "!isEdit">
            <div class="main" v-if="link === 'all'">
                <ul>
                    <li v-for="item in props.content" :key="item.id" class="item">
                        <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit" />
                    </li>
                </ul>
            </div>
            <div class="main" v-else-if="link === 'completed'">
                <ul>
                    <template v-for="item in props.content" :key="item.id">
                        <li v-if="item.isDone" class="item">
                            <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit" />
                        </li>
                    </template>
                </ul>
            </div>
            <div class="main" v-else="link === 'ongoing' ">
                <ul>
                    <template v-for="item in props.content" :key="item.id">
                        <li v-if="!item.isDone" class="item">
                            <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit"/>
                        </li>
                    </template>
                </ul>
            </div>
        </div>
        <div v-if="isEdit">
            <NewFile :inputValue="inputValue" :textValue="textValue" :id="id" @update="handleReset"/>
        </div>

    </div>
</template>
<style scoped>
.item{
    padding: 0px 10px;
}
.active {
    text-decoration: underline;
}

.all {
    width: 600px;
}

.main {
    margin: auto;
}

ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

li {
    margin: 15px auto;
}

.container {
    display: flex;
    justify-content: space-between;
}

.title {
    font-size: medium;
}
</style>