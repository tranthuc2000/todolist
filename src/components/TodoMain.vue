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
    <div >
        <div class="flex justify-between m-6" v-show="!isEdit">
            <div class="flex-initial mx-4" @click="link = 'all'" :class="{ 'active': link === 'all' }">{{ title.all }}</div>
            <div class="flex-initial mx-4" @click="link = 'completed'" :class="{ 'active': link === 'completed' }">{{ title.complete }}</div>
            <div class="flex-initial mx-4" @click="link = 'ongoing'" :class="{ 'active': link === 'ongoing' }">{{ title.ongoing }}</div>
        </div>
        <div v-if = "!isEdit" >
            <div  v-if="link === 'all'">
                <ul>
                    <li v-for="item in props.content" :key="item.id" class="m-4">
                        <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit" />
                    </li>
                </ul>
            </div>
            <div  v-else-if="link === 'completed'">
                <ul>
                    <template v-for="item in props.content" :key="item.id">
                        <li v-if="item.isDone" class="m-4">
                            <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit" />
                        </li>
                    </template>
                </ul>
            </div>
            <div  v-else="link === 'ongoing' ">
                <ul>
                    <template v-for="item in props.content" :key="item.id">
                        <li v-if="!item.isDone" class="m-4">
                            <TodoItem :content="item" @update="handleIsDone" @delete="handleDel" @edit ="handleEdit"/>
                        </li>
                    </template>
                </ul>
            </div>
        </div>
    </div>
    <div v-if="isEdit" class="w-4/5 flex justify-center">
            <NewFile :inputValue="inputValue" :textValue="textValue" :id="id" @update="handleReset"/>
        </div>
</template>