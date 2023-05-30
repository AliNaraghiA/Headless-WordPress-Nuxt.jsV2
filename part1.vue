<template>
  <div class="gallery">
    <div class="enGallery mont" v-if="language == 'en'">
      <Header lang="eng" @change="change" />
      <div class="topDiv">
        <h3>Gallery</h3>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
          eiusmod tempor incididunt ut labore et dolore magna aliqua Egestas
          purus viverra accumsan in nisl nisi Arcu cursus.
        </p>
      </div>
      <div class="galleryList">
        <div class="imageDiv" v-for="i in 9" :key="i">
          <img src="/images/businessUnit.jpg" alt="gallery" />
          <div class="text">لورم ایپسوم متن ساختگی با تولید</div>
        </div>
      </div>
      <Footer lang="en" />
    </div>
    <div class="faGallery irancell" v-else>
      <Header lang="fa" @change="change" />
      <div class="topDiv">
        <h3 class="mont">Gallery</h3>
        <p>
          لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده
          از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و
          سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز.
        </p>
      </div>
      <div class="galleryList">
        <div class="imageDiv">
          <ul>
        <li v-for="item in acrepeater" :key="item.acemage.ID">
          <img :src="item.acemage.url" :alt="item.acemage.alt">
          <h2> {{ item.aclink }}</h2>
        </li>
      </ul>
        </div>
      </div>
      <Footer lang="fa" />
    </div>
    <MouseEffect />
  </div>
</template>

<script>
export default {
  data() {
    return {
      language: "",
    };
  },
  mounted() {
    this.language = this.$store.state.lang;
  },
  methods: {
    change() {
      this.$store.commit("change");
    },
  },
  watch: {
    "$store.state.lang"() {
      this.language = this.$store.state.lang;
    },
  },
  //dynamic
      data() {
      return {
        cptgalleryone: []
      }
    },
    computed: {
      acrepeater() {
        return this.cptgalleryone[0]?.acf?.acrepeater || []
      }
    },
    async fetch() {
      this.cptgalleryone = await fetch('http://nuxtwp.local/wp-json/acf/v3/cptgalleryone').then(res => res.json())
    }
};
</script>

<style>
</style>