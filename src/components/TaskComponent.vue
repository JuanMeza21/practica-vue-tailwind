<script setup>
import { ref, defineProps } from 'vue';

const text = ref('');
const completedMessage = ref('');
let checkboxRef = ref('')
const emit = defineEmits(['deleteTask'])

const props = defineProps({
    message: {
        type: String,
        default: 'No message',
    },
    date: {
        type: Date,
        default: 'No date',
    },
    index: {
        type: Number,
    },
});

const check = () => {
    if (checkboxRef.value.checked) {
        text.value = 'text-decoration-line: line-through; font-weight: bold;';
        completedMessage.value = 'Completed';
    } else {
        text.value = '';
        completedMessage.value = 'Imcompleted';
    }
};

const deleteTask = (index) => {
    emit('deleteTask', index)
}
</script>


<template>
    <div class="shadow px-4 py-2">
        <span v-if="completedMessage === 'Completed'" class="pr-4 font-semibold text-green-700 float-left">
            {{ completedMessage }}
        </span>

        <span v-else-if="completedMessage === 'Imcompleted'" class="pr-4 font-semibold text-red-500 float-left">
            {{ completedMessage }}
        </span>

        <div>
            <span :style="text" class="text-lg">{{ props.message }}</span>

            <button @click="deleteTask(props.index)"
                class="float-right ml-4 w-5 h-5 flex justify-center items-center text-center cursor-pointer">
                <img src="../assets/imgs/remove.png" alt="">
            </button>

            <input ref="checkboxRef" @click="check"
                class="float-right ml-4 w-5 h-5 flex justify-center items-center text-center" type="checkbox" />

            <span class="text-lg font-bold float-right">Deadline: {{ props.date }}</span>
        </div>
    </div>
</template>

<style scoped></style>