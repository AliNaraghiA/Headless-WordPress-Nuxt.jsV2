<template>
    <div>
      <ul>
        <li v-for="post in posts.edges" :key="post.node.databaseId">
          <h2>{{ post.node.title }}</h2>
          <p v-html="post.node.excerpt"></p>
          <img v-if="post.node.featuredImage" :src="post.node.featuredImage.node.sourceUrl" />
        </li>
      </ul>
      <button @click="previousPage" :disabled="page === 1">Previous Page</button>
      <button @click="nextPage" :disabled="!posts.pageInfo.hasNextPage">Next Page</button>
    </div>
  </template>
<script>
import gql from 'graphql-tag'
export default{
data() {
    return {
      posts: [],
      page: 1,
      pageSize: 5,
    };
  },
  apollo: {
    posts: {
      query: gql`
        query Posts($first: Int, $after: String) {
          posts(first: $first, after: $after) {
            pageInfo {
              endCursor
              hasNextPage
              hasPreviousPage
            }
            edges {
              node {
                databaseId
                title
                slug
                excerpt
                featuredImage {
                  node {
                    sourceUrl
                  }
                }
              }
            }
          }
        }
      `,
      variables() {
        return {
          first: this.pageSize,
          after: '',
        };
      },
    },
  },
  methods: {
    nextPage() {
      if (this.posts.pageInfo.hasNextPage) {
        this.page++;
        this.fetchMorePosts(this.posts.pageInfo.endCursor);
      }
    },
    previousPage() {
      if (this.page > 1) {
        this.page--;
        this.fetchMorePosts(this.posts.pageInfo.startCursor, true);
      }
    },
    fetchMorePosts(cursor, isPrevious = false) {
      this.$apollo.queries.posts.fetchMore({
        variables: {
          first: this.pageSize,
          after: cursor,
        },
        updateQuery: (previousResult, { fetchMoreResult }) => {
          this.posts = fetchMoreResult.posts;
        },
      });
    },
  },
};
</script>
