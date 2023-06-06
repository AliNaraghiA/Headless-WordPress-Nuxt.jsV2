<template>
    <div>
      <h1>My Blog</h1>
      <ul>
        <li v-for="post in posts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p>{{ post.title }}</p>
        </li>
      </ul>
      <div>
        <nuxt-link v-if="previousPage" :to="previousPage">Previous Page</nuxt-link>
        <nuxt-link v-if="nextPage" :to="nextPage">Next Page</nuxt-link>
      </div>
    </div>
    </template>
<script>
 export default {
    data() {
      return {
        posts: [],
        currentPage: 1,
        postsPerPage: 10,
        totalPosts: 0
      }
    },
    async asyncData({ $axios }) {
      const response = await $axios.get('http://nuxtwp.local/wp-json/wp/v2/posts')
      const posts = response.data
      const totalPosts = posts.length
      return { posts, totalPosts }
    },
    computed: {
      totalPages() {
        return Math.ceil(this.totalPosts / this.postsPerPage)
      },
      previousPage() {
        return this.currentPage > 1 ? `/page/${this.currentPage - 1}` : null
      },
      nextPage() {
        return this.currentPage < this.totalPages ? `/page/${this.currentPage + 1}` : null
      }
    },
    mounted() {
      this.posts = this.posts.slice(0, this.postsPerPage)
    }
  }
  
</script>
 
