<template>
    <div class="container">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <h1 class="mt-4">Seznam článků</h1>
                <div v-for="post in posts" :key="post.id" class="mb-4">
                    <img :src="post.image" alt="Obrázek článku" class="img-fluid" />
                    <h2>{{ post.title }}</h2>
                    <p class="text-muted">{{ post.createdAt }}</p>
                    <p>{{ post.content }}</p>  
                    <router-link :to="'/post/' + post.id" class="btn btn-primary">Přejít na detail</router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    async asyncData({ $axios }) {
        try {
            const response = await $axios.get('/posts')
            return { posts: response.data }
        } catch (error) {
            console.error('Chyba při načítání článků', error)
            return { posts: [] }
        }
    }
}
</script>
