<script setup lang="ts">
import { ref } from 'vue'

const title = 'Random String';
const options = [
  {
    text: 'Uppercase (A-Z)',
    value: 'uppercase',
  },
  {
    text: 'Lowercase (a-z)',
    value: 'lowercase',
  },  
  {
    text: 'Digit (0-9)',
    value: 'digit'
  },
  {
    text: 'Special characters',
    value: 'special'
  },
  {
    text: 'Space',
    value: 'space'
  }
]

const newString = ref('');
const stringLength = ref(20);
const pickedOptions = ref([]);

const generateString = () => {
  if (stringLength.value > 0) {
    let chars = '';
    for (let optionIndex in pickedOptions.value) {
      const optionValue = pickedOptions.value[optionIndex];
      let index = options.findIndex((o) => o.value === optionValue);
      switch(index) {
        case 0:
          chars += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
          break;
        case 1:
          chars += 'abcdefghijklmnopqrstuvwxyz';
          break;
        case 2:
          chars += '0123456789';
          break;
        case 3:
          chars += "!\"#$ %&'()*+,-./:;<=>?@[\]^_`{|}~";
          break;
        case 4:
          chars += ' ';
          break;
        default:
          break;
      }
    }

    if (chars.length > 0) {
      let result = [];

      let arr = new Uint8Array(stringLength.value);
      window.crypto.getRandomValues(arr);
      for (let i = 0; i < arr.length; i += 1) {
          let charIndex = Math.floor(arr[i] / 256 * chars.length);
          result.push(chars.charAt(charIndex));
      }

      newString.value = result.join('');
    }
  }
}
</script>

<template>
  <ToolContainer>
    <PageHeader :title="title" />
    <div class="container-fluid">
      <div class="row">
        <div class="col-auto">
          <label for="length" class="col-form-label">Length</label>
        </div>
        <div class="col-auto">
          <input type="number" id="length" class="form-control" aria-describedby="length" v-model="stringLength"/>
        </div>
      </div>
      <div class="row row-cols-2 mt-3">
        <div class="col" v-for="option in options">

          <div class="form-check">
            <input class="form-check-input" type="checkbox" :value="option.value" :id="option.value" v-model="pickedOptions">
            <label class="form-check-label" :for="option.value">
              {{ option.text }}
            </label>
          </div>

        </div>
      </div>
      <div class="row mt-3">
        <div class="col d-grid">
          <button class="btn btn-primary" @click="generateString">Generate String</button>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <ToolOutput :output-value="newString"/>
        </div>
      </div>
    </div>
  </ToolContainer>
</template>