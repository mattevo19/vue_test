<script setup>
import { reactive, computed } from "vue"
defineProps({
  post: {
    title: {
      type: String
    },
    id: {
      type: Number
    },
    type: Object,
    required: false
  }
})
const author = reactive({
  cursor: ["help", "wait", "grab", "copy", "cell", "pointer", "move", "zoom-out", "zoom-in"],
  selectedBook: 0,
  cart: 0,
  firstName: "Matt",
  lastName: "Masciave",
  show: true,
  books: [
    {
      title: "Vue 1 - Starter Guide",
      id: 0,
      color: "pink",
      quantity: 5,
      url: "https://images.unsplash.com/photo-1574158622682-e40e69881006?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1480&q=80"
    },
    {
      title: "Vue 2 - Advanced Guide",
      id: 1,
      color: "blue",
      quantity: 50,
      url: "https://images.unsplash.com/photo-1495360010541-f48722b34f7d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1036&q=80"
    },
    {
      title: "Vue 3 - Basic Guide",
      id: 2,
      color: "red",
      quantity: 0,
      url: "https://images.unsplash.com/photo-1526336024174-e58f5cdd8e13?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80"
    },
    {
      title: "Vue 4 - The Mystery",
      id: 3,
      color: "orange",
      quantity: 10,
      url: "https://images.unsplash.com/photo-1618826411640-d6df44dd3f7a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=987&q=80"
    }
  ]
})

const title = computed(() => {
  return author.firstName + " " + author.lastName
})

const randomCursor = () => {
  return author.cursor[Math.floor(Math.random() * author.cursor.length)]
}

const addToCart = () => {
  author.cart += 1
}

const removeFromCart = () => {
  author.cart -= 1
}

const updateBook = (index) => {
  author.selectedBook = index
}
const image = computed(() => {
  return author.books[author.selectedBook].url
})
const publishedBooksMessage = () => {
  return author.books.length > 0 ? "Yes" : "No"
}

const now = () => {
  const date = new Date()
  return date.toDateString()
}
</script>

<template>
  <div :style="{ cursor: randomCursor() }">
    <p>{{ title }}</p>
    <p>{{ post.title }}</p>

    <img class="size" v-bind:src="image" />

    <div v-for="book in author.books" :key="book.id">
      <h3>{{ book.title }}</h3>
    </div>

    <div
      class="circle"
      v-for="(book, index) in author.books"
      @mouseover="updateBook(index)"
      :key="book.id"
      :style="{ backgroundColor: book.color }"
    />

    <p v-if="author.show">SHOW ME IF TRUE</p>
    <p v-else>SHOW ME IF FALSE</p>

    <p>Has published books:</p>
    <span>{{ publishedBooksMessage() }}</span>
    <p>{{ now() }}</p>

    <span class="padding">Cart {{ author.cart }}</span>
    <button @click="addToCart" :disabled="author.cart === 5" :class="{ disabled: author.cart === 5 }">
      Add to cart
    </button>
    <button @click="removeFromCart" :disabled="author.cart === 0" :class="{ disabled: author.cart === 0 }">
      Remove from to cart
    </button>
  </div>
</template>

<style scoped>
.size {
  height: 500px;
}
.padding {
  padding-right: 10px;
}

.disabled {
  cursor: not-allowed;
}
.circle {
  height: 50px;
  width: 50px;
  border-radius: 50%;
  border: 1px solid black;
  margin: 2px;
}
</style>
