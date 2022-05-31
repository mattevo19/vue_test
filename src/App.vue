<script setup>
import Hi from "./components/Hi.vue"
import Books from "./components/Books.vue"

const props = {
  id: 1,
  title: "hello props"
}
</script>

<template>
  <Hi />
  <Books :post="props" />
</template>

<style></style>
