<template>
    <div>
      <h1>My Blog</h1>
      <ul>
        <li v-for="post in posts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p>{{ post.title }}</p>
          <p>{{totalPosts}}</p>
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
        postsPerPage: 5,
        totalPosts: 0
      }
    },
    async asyncData({ $axios }) {
      const response = await $axios.get('http://nuxtwp.local/wp-json/wp/v2/posts?per_page=100&_embed')
      const posts = response.data
      const totalPosts = posts.length
      return { posts, totalPosts }
    },
/*     fetch('https://your-wordpress-site.com/wp-json/wp/v2/posts?_embed')
  .then(response => response.json())
  .then(posts => {
    posts.forEach(post => {
      const imageUrl = post._embedded['wp:featuredmedia'][0].source_url
      console.log(imageUrl)
    })
  })
  .catch(error => {
    console.error(error)
  }) */
    computed: {
      totalPages() {
        return Math.ceil(this.totalPosts / this.postsPerPage)
      },
      previousPage() {
        return this.currentPage > 1 ? `/test/test18/${this.currentPage - 1}` : null
      },
      nextPage() {
        return this.currentPage < this.totalPages ? `/test/test18/${this.currentPage + 1}` : null
      }
    },
    mounted() {
      this.posts = this.posts.slice(0, this.postsPerPage)
    }
  }
  
</script>
 
 
 
 
 
// ~_id
<template>
    <div>
      <h1>My Blog</h1>
      <ul>
        <li v-for="post in displayedPosts" :key="post.id">
          <h2>{{ post.title }}</h2>
          <p>{{ totalPosts }}</p>
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
        postsPerPage: 5,
        totalPosts: 0
      }
    },
    async asyncData({ $axios, params }) {
      const response = await $axios.get('http://nuxtwp.local/wp-json/wp/v2/posts?per_page=100&_embed')
      const posts = response.data
      const totalPosts = posts.length
      const currentPage = parseInt(params.id)
      return { posts, totalPosts, currentPage }
    },
    computed: {
      totalPages() {
        return Math.ceil(this.totalPosts / this.postsPerPage)
      },
      displayedPosts() {
        const startIndex = (this.currentPage - 1) * this.postsPerPage
        const endIndex = startIndex + this.postsPerPage
        return this.posts.slice(startIndex, endIndex)
      },
      previousPage() {
        return this.currentPage > 1 ? `/test/test18/${this.currentPage - 1}` : null
      },
      nextPage() {
        return this.currentPage < this.totalPages ? `/test/test18/${this.currentPage + 1}` : null
      }
    },
    mounted() {
      this.posts = this.posts.slice(0, this.totalPosts)
    }
  }
  </script>
  
