<script setup lang="ts">
import { provide } from 'vue'
import type { ToolCategory } from './models/tool-category'

const toolkit: ToolCategory[] = [
  {
    title: "Converters",
    url: "/converters",
    tools: [
      {
        name: "Letter case",
        url: "/converter/lettercase"
      }
    ]
  },
  {
    title: "Encoders",
    url: "/encoders",
    tools: [
      {
        name: "URL",
        url: "/encoder/url"
      },
      {
        name: "Base64",
        url: "/encoder/base64"
      }
    ]
  },
  {
    title: "Generators",
    url: "/generators",
    tools: [
      {
        name: "UUID",
        url: "/generator/uuid"
      },
      {
        name: "Random String",
        url: "/generator/random-string"
      }
    ]
  }
]

provide('toolkit', toolkit)
</script>

<template>
  <div class="d-flex flex-column vh-100">
    <nav class="navbar navbar-expand-lg bg-dark" data-bs-theme="dark">
      <div class="container-fluid">
        <NuxtLink to="/" class="navbar-brand">WebToolkit</NuxtLink>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav me-auto">
            <li class="nav-item dropdown" v-for="category in toolkit">
              <a href="#" class="nav-link dropdown-toggle" role="button" data-bs-toggle="dropdown" aria-expanded="false">{{ category.title }}</a>
              <ul class="dropdown-menu">
                <li v-for="tool in category.tools">
                  <NuxtLink :to="tool.url" class="dropdown-item">{{ tool.name }}</NuxtLink>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div class="bg-body-secondary p-3 flex-grow-1">
      <NuxtPage />
    </div>
  </div>
</template>
