<script setup>
import { ref } from 'vue'

const props = defineProps({
  inputValue: String,
  enablePaste: {
    type: Boolean,
    default: false,
    required: false
  }
})

//https://vuejs.org/guide/components/v-model.html#v-model-arguments
const emit = defineEmits(['update:inputValue']);

const inputRef = ref(props.inputValue);
const isPasted = ref(false);

const paste = () => {
  navigator.clipboard
    .readText()
    .then(
      (value) => {
        inputRef.value = value;
        isPasted.value = true;
        setTimeout(() => isPasted.value = false, 500);
      })  
}

const handleChange = (event) => {
  if (event.target.value) {
    emit('update:inputValue', event.target.value);
  }  
} 
</script>

<template>
  <div v-if="enablePaste" class="input-group">
    <input type="text" class="text-black text-center form-control border border-secondary" v-model="inputRef" :title="inputRef" @change="handleChange"/>
    <button v-if="isPasted" class="btn btn-secondary">Pasted</button>
    <button v-else class="btn btn-secondary" @click="paste">Paste</button>
  </div>
  <div v-else>
    <input type="text" class="text-black text-center form-control border border-secondary" v-model="inputRef" :title="inputRef" @change="handleChange"/>
  </div>
</template>