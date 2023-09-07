<template>
    <div>
      <div v-for="comment in comments" :key="comment.id" class="mb-3">
        <div class="media">
          <img :src="comment.avatar" alt="Avatar" class="mr-3" />
          <div class="media-body">
            <h5 class="mt-0">{{ comment.name }}</h5>
            <p class="text-muted">{{ comment.createdAt }}</p>
            <p>{{ comment.comment }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      postId: Number
    },
    data() {
      return {
        comments: []
      }
    },
    async created() {
      if (this.postId) {
        await this.loadComments()
      }
    },
    methods: {
      async loadComments() {
        try {
          const response = await this.$axios.get(`/comments?postId=${this.postId}`)
          this.comments = response.data
        } catch (error) {
          console.error('Chyba při načítání komentářů', error)
        }
      }
    }
  }
  </script>
  