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
    <div class="newfile">
        <div class="title">
            Title
        </div>
        <input type="text" v-model="inputValue" required>
        <div class="title">
            Details
        </div>
        <textarea v-model="textValue" required></textarea>
        <div class="add"><button @click="updateValue">Add Project</button> </div>
    </div>
</template>
<style>
.title {
    padding: 10px;
    font-size: 20px;
}

.newfile {
    
    width: 600px;
    border-radius: 3px;
    background-color: aliceblue;
}

input {
    margin: 0px 40px;
    width: 460px;
    height: 30px;
}

textarea {
    margin: 0px 40px;
    width: 460px;
    height: 100px
}

.add {
    text-align: center;

}

button {
    margin: 20px;
    height: 30px;
    border: 3px;
    border-radius: 3px;
    color: white;
    background-color: green;
}</style>