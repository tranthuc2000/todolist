<script setup>
import { ref } from 'vue'

const isActive = ref(false)
const props = defineProps(['content'])
const emit = defineEmits(['update','delete','edit'])

const changeState = () =>{
    const isdone = !props.content.isDone
    emit('update',{id: props.content.id, isDone: isdone})
}

const onDelete = () =>{
   emit('delete',props.content.id)
}

const onEdit = () => {
    emit('edit',props.content)
}
</script> 
<template>
    <div class=" bg-gray-100 rounded " :style="{borderLeft: props.content.isDone ? '7px solid green' :'7px solid red'}">
        <div class="h-12 flex items-center justify-between flex-grow pl-4 overflow-y-scroll" >
                <div class="flex-initial">
                    <h3  @click="isActive = !isActive">{{ props.content.title }}</h3>
                </div>
                    <div class=" flex-initial flex-none">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960" class="icon inline" @click="onEdit">
                            <path
                                d="M200-200h57l391-391-57-57-391 391v57Zm-80 80v-170l528-527q12-11 26.5-17t30.5-6q16 0 31 6t26 18l55 56q12 11 17.5 26t5.5 30q0 16-5.5 30.5T817-647L290-120H120Zm640-584-56-56 56 56Zm-141 85-28-29 57 57-29-28Z" />
                        </svg>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960" class="icon inline " @click="onDelete">
                            <path
                                d="M280-120q-33 0-56.5-23.5T200-200v-520h-40v-80h200v-40h240v40h200v80h-40v520q0 33-23.5 56.5T680-120H280Zm400-600H280v520h400v-520ZM360-280h80v-360h-80v360Zm160 0h80v-360h-80v360ZM280-720v520-520Z" />
                        </svg>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 -960 960 960" class="inline" @click="changeState" :style=" { fill: props.content.isDone ? 'green' : 'black'} ">
                            <path d="M382-240 154-468l57-57 171 171 367-367 57 57-424 424Z" />
                        </svg>
                    </div>
        </div>
        <div class=" m-1 overflow-y-auto" v-if="isActive">{{ props.content.content }}</div>
    </div>
    
</template>
<style scoped>


svg {
    height: 30px;
    width: 30px;
}
</style>