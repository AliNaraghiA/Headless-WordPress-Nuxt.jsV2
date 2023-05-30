
<template>
    <div>
      <p v-if="$fetchState.pending">Loading....</p>
      <p v-else-if="$fetchState.error">Error while fetching cptpost</p>
      <ul v-else>
        <li v-for="(cptpos, index) in cptpost" :key="index">
          {{ cptpos.acf.ptext}}
          <img :src="cptpos.acf.pimage.url" :alt="cptpos.acf.pimage.alt" />
          <div v-html='cptpos.acf.ptextarea'></div>

        </li>
        
       
      </ul>
    </div>
  </template>
  <script>
    export default {
      data() {
        return {
            cptpost: []
        }
      },
      async fetch() {
        this.cptpost = await fetch(
          'http://nuxtwp.local/wp-json/acf/v3/cptpost?per_page=3'
        ).then(res => res.json())
      }
    }
    //http://nuxtwp.local/wp-json/acf/v3/cptpost?per_page=3
  </script>