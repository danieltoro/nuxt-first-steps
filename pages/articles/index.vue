<template>
  <div class="container">
    <div v-for="(item, index) in articles" :key="index" class="card mt-4">
      <div class="card-body">
        <nuxt-link :to="`/articles/${item.id}`">
          <h1>{{ item.title }}</h1>
        </nuxt-link>
        <p>{{ item.body }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData ({ params }) {
    try {
      const res = await axios.get(
        'https://jsonplaceholder.typicode.com/posts?_limit=15'
      )
      const articles = res.data

      return { articles }
    } catch (error) {
      return { error }
    }
  }
}
</script>
