<template>
    <div>
      <input type="text" v-model="searchQuery" @input="searchPosts" placeholder="Search..." />
      <div v-if="searchResults.length > 0">
        <div v-for="post in searchResults" :key="post.id">
          <nuxt-link :to="'/post/' + post.slug">{{ post.title.rendered }}</nuxt-link>
        </div>
      </div>
    </div>
  </template>
<script>
export default {
  data() {
    return {
      searchQuery: '',
      searchResults: [],
    };
  },
  methods: {
    async searchPosts() {
      if (this.searchQuery.length > 2) {
        try {
          const response = await this.$axios.get(
            `http://nuxtwp.local/wp-json/wp/v2/posts?search=${this.searchQuery}&_embed`
          );
          this.searchResults = response.data;
        } catch (error) {
          console.error('Error fetching search results:', error);
        }
      } else {
        this.searchResults = [];
      }
    },
  },
};
</script>
  
