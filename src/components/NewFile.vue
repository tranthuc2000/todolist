<script setup>
import { onMounted, watch, ref, onUpdated, onBeforeUpdate } from 'vue';

const emit = defineEmits(['update'])
const props = defineProps({
    id: {
        type: Number,
        default: 0
    },
    inputValue: {
        type: String,
        default: ''
    },
    textValue: {
        type: String,
        default: ''
    }
})
const id =ref(props.id)
const inputValue = ref(props.inputValue);
const textValue = ref(props.textValue);

const updateValue = () => {
    if (!inputValue.value || !textValue.value) {
        alert('Please fill in all required fields.');
        return;
    }
    emit('update', { id: id.value,content: textValue.value, title: inputValue.value, })
    textValue.value = ''
    inputValue.value = ''
}
</script>
<template >
    <div class="bg-gray-100 w-3/5  ">
        <div class="m-4 text-lg">
            Title
        </div >
        <input  class="ml-4 h-10 w-4/5" type="text" v-model="inputValue" required>
        <div class="m-4 text-lg">
            Details
        </div>
        <textarea class="ml-4 h-40 w-4/5"  v-model="textValue" required></textarea>
        <button class="flex justify-center mx-auto my-2 bg-green-500 w-32 h-10 py-2 border border-gray-300 rounded" @click="updateValue">Add Project</button> 
    </div>
</template>