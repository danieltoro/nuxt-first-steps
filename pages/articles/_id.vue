<template>
  <div class="container">
    <h1>Post {{ article.title }}</h1>
    <p class="small">
      Author: {{ article.nombreAuthor }}
    </p>
    <p>{{ article.body }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData ({ params }) {
    try {
      const res = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${params.id}`
      )
      const article = res.data

      const resAuthor = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${res.data.userId}`
      )

      article.nombreAuthor = resAuthor.data.name

      return {
        article
      }
    } catch (error) {
      return { error }
    }
  }
}
</script>
