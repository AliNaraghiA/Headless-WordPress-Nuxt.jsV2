// _slug/index.vue
<template>
     <div>
       <h1>All Posts</h1>
       <ul>
         <li v-for="post in posts" :key="post.id">
           <nuxt-link :to="`/${post.slug}`">{{ post.title }}</nuxt-link>
         </li>
       </ul>
     </div>
   </template>
//---------------------
   <script>
   export default {
     async asyncData({ params, $axios }) {
       const { slug } = params;
       const post = await $axios.$get(`/api/posts/${slug}`);
       return { post };
     },
   };
   </script>
//--------------------------
