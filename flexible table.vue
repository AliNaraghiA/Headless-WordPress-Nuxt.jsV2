<template>
   <div>
      <h1>{{ industrial?.acfindustrial?.title }}</h1>
      <p>{{ industrial?.acfindustrial?.description }}</p>
      <div class="gallery">
        <div v-for="(image, index) in industrial?.acfindustrial?.gallery" :key="index">
          <img :src="image.sourceUrl" />
      </div>
      </div>
  <table>
     <tbody>
       <tr v-for="row in tableData" :key="row">
         <td v-for="name in row" :key="name">{{ name }}</td>
       </tr>
     </tbody>
   </table>

      </div>
  </template>
  
  <script>
 import indust from '~/apollo/queries/indust.gql'
  export default {
   async asyncData({ app, params }) {
      const { data } = await app.apolloProvider.defaultClient.query({
        query:indust,
        variables: {
          id: params.id,
        },
      })
      return {
        industrial: data.industrial,
      }
    },
//table

  computed: {
     tableData() {
       const names = this.industrial.acfindustrial.repeater.map((item) => item.one);
       const maxNamesPerRow = 10;
       const rows = [];
       for (let i = 0; i < names.length; i += maxNamesPerRow) {
         rows.push(names.slice(i, i + maxNamesPerRow));
       }
       return rows;
     },
   },
    };
  </script>
