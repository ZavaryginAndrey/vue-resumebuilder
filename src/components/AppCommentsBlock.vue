<template>
  <div class="container">
    <app-loader v-if="loading"></app-loader>
    <div class="loader" v-if="loading"></div>
    <p v-else-if="!comments.length && !loading">
      <button
        class="btn primary"
        @click="loadComments"
      >Загрузить комментарии</button>
    </p>
    <div class="card" v-else>
      <h2>Комментарии</h2>
      <ul class="list">
        <app-comment
          v-for="comment in comments"
          :comment="comment"
        ></app-comment>
      </ul>
    </div>
  </div>
</template>

<script>
import AppComment from '@/components/AppComment'
import AppLoader from '@/components/AppLoader'
import axios from 'axios'

export default {
  data() {
    return {
      loading: false,
      comments: []
    }
  },
  props: ['url'],
  methods: {
    async loadComments() {
      try {
        this.loading = true
        const {data} = await axios.get(this.url)
        this.comments = data
      }
      catch (e) {
        this.comments = [{
          email: 'Something went wrong'
        }]
      }
      finally {
        this.loading = false
      }
    }
  },
  components: {
    AppComment,
    AppLoader
  }
}
</script>

<style scoped>

</style>