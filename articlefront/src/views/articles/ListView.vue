<template>
  <div class="container">
      <h1>Article List</h1>
      <button @click="create">글쓰기</button>
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">제목</th>
            <th scope="col">작성자</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="article in articles" :key="`article_${article.id}`">
            <th scope="row">{{ article.id }}</th>
            <td>{{ article.title }}</td>
            <td>{{ article.user.username }}</td>
          </tr>
        </tbody>
      </table>
  </div>
</template>

<script>
import axios from 'axios'

const SERVER_URL = "http://127.0.0.1:8000"
export default {
    name: 'ListView',
    data() {
        return {
            articles: []
        }
    },
    methods: {
        fetchArticles() {
            axios.get(SERVER_URL + '/articles/')
              .then(res => this.articles = res.data)
              .catch(err => console.error(err))
        },
        create() {
          this.$router.push({ name: 'Create' })
        },
    },
    created() {
        this.fetchArticles()
    },
}
</script>

<style>

</style>