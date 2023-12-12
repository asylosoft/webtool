<script setup lang="ts">
import { ref } from 'vue'
import jmespath from 'jmespath'

const title = 'JMESPath';

const inputJson = ref('');
const outputJson = ref('');
const expression = ref('');

const query = () => {
  if (inputJson.value && expression.value) {
    const inputJsonObject = JSON.parse(inputJson.value);
    outputJson.value = jmespath.search(inputJsonObject, expression.value);
  }
}
</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col col-sm-10 offset-sm-1 col-md-8 offset-md-2 col-lg-6 offset-lg-3 col-xl-4 offset-xl-4">

        <PageHeader :title="title" />
        <div class="container-fluid">
          <div class="row">
            <div class="col">
              <ToolInput v-model:input-value="inputJson" :multiline="true"/>
            </div>
          </div>
          <div class="row mt-3">
            <div class="col-auto">
              <label for="length" class="col-form-label">Query</label>
            </div>
            <div class="col">
              <input type="text" class="form-control" aria-describedby="length" v-model="expression"/>
            </div>
          </div>
          <div class="row mt-3">
            <div class="d-grid col">
              <button class="btn btn-primary" @click="query">Run</button>
            </div>
          </div>
          <div class="row mt-3">
            <div class="col">
              <ToolOutput :output-value="outputJson" :multiline="true"/>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>