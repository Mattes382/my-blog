<template>
    <div class="container">
      <div class="row">
        <div class="col-md-8 offset-md-2">
          <h1 class="mt-4">{{ post.title }}</h1>
          <p class="text-muted">{{ post.createdAt }}</p>
          <img :src="post.image" alt="Obrázek článku" class="img-fluid mb-4" />
          <p class="lead">{{ post.content }}</p>
          <hr />
          <h2 class="mb-3">Komentáře</h2>
          <comments :postId="post.id"></comments>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Comments from '~/components/Comments.vue'
  
  export default {
    components: {
      Comments
    },
    async asyncData({ params, $axios }) {
      try {
        const response = await $axios.get(`/posts/${params.id}`)
        return { post: response.data }
      } catch (error) {
        console.error('Error loading post', error)
        return { post: {} }
      }
    }
  }
  </script>
  