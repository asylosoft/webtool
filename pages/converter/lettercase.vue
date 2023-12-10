<script setup lang="ts">
import { ref } from 'vue'

const title = 'Letter case';

const inputString = ref('');
const outputString = ref('');
const lettercases = [
  'lowercase',
  'UPPERCASE',
  'camelCase',
  'PascalCase',
  'none'
];
const delimitercases = [
  'none',
  'kebab-case',
  'snake_case'
]
const pickedLetterCase = ref(lettercases[0]);
const pickedDelimiterCase = ref (delimitercases[0]);

const wordPattern = /(?:^\w|[A-Z]|\b\w)/g
const spacesPattern = /\s+/g

const convert = () => {
  if (inputString.value) {
    let outputValue = inputString.value;

    const letterIndex = lettercases.indexOf(pickedLetterCase.value);
    switch(letterIndex) {
      case 0:
        outputValue = inputString.value.toLowerCase();
        break;
      case 1:
        outputValue = inputString.value.toUpperCase();
        break;
      case 2:
        outputValue = inputString.value.replace(wordPattern, (word, index) => {
                                return index === 0 ? word.toLowerCase() : word.toUpperCase();
                              }).replace(spacesPattern, '');
        break;
      case 3:
        outputValue = inputString.value.replace(wordPattern, (word, index) => {
                                return word.toUpperCase();
                              }).replace(spacesPattern, '');
        break;
      default:
        break;
    }

    const delimiterIndex = delimitercases.indexOf(pickedDelimiterCase.value);
    switch(delimiterIndex) {
      case 1:
        outputValue = outputValue.replace(wordPattern, (word, index) => {
                                return index === 0 ? word : ` ${word}`;
                              }).replace(spacesPattern, '-');
        break;
      case 2:
        outputValue = outputValue.replace(wordPattern, (word, index) => {
                                return index === 0 ? word : ` ${word}`;
                              }).replace(spacesPattern, '_');
        break;
      default:
        break;
    }
    
    outputString.value = outputValue;
  }
}
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col col-sm-10 offset-sm-1 col-md-8 offset-md-2 col-lg-6 offset-lg-3 col-xl-4 offset-xl-4">
        
        <PageHeader :title="title" />
        <div class="container-fluid text-center">
          <div class="row">
            <div class="col">
              <ToolInput v-model:input-value="inputString"/>
            </div>
          </div>
          <div class="row mt-3">
            <div class="d-grid col">
              <button class="btn btn-primary" @click="convert">Convert</button>
            </div>
          </div>
          <div class="row text-start mt-3">
            <div class="col px-3">
              <label><em>Letter:</em></label>
            </div>
          </div>
          <div class="row row-cols-2 text-start mt-1">
            <div class="col" v-for="lettercase in lettercases">
              <div class="form-check">
                <input class="form-check-input" type="radio" name="lettercase" 
                  :id="lettercase" 
                  :value="lettercase" 
                  v-model="pickedLetterCase">
                <label class="form-check-label" :for="lettercase">
                  {{ lettercase }}
                </label>
              </div>
            </div>
          </div>
          <div class="row text-start mt-3">
            <div class="col px-3">
              <label><em>Delimiter:</em></label>
            </div>
          </div>
          <div class="row row-cols-2 text-start mt-1">
            <div class="col" v-for="delimitercase in delimitercases">
              <div class="form-check">
                <input class="form-check-input" type="radio" name="delimitercase" 
                  :id="delimitercase" 
                  :value="delimitercase" 
                  v-model="pickedDelimiterCase">
                <label class="form-check-label" :for="delimitercase">
                  {{ delimitercase }}
                </label>
              </div>
            </div>
          </div>
          <div class="row mt-3">
            <div class="col">
              <ToolOutput :output-value="outputString"/>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>