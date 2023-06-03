<template>

    <div class="blogs">
      <div class="enBlogs mont" v-if="language == 'en'">
        <Header lang="eng" @change="change" />
        <div class="topDiv">
          <h3>Blog</h3>
          <h1>Every Things About Aluminium.</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
            eiusmod tempor incididunt ut labore et dolore magna aliqua Egestas
            purus viverra accumsan in nisl nisi Arcu cursus.
          </p>
        </div>
        <div class="lineDiv">
          <Lines myVw="1920" myVh="360" />
        </div>
        <div class="blogList">
          <div
            class="d-flex justify-content-between blog"
            v-for="item in blogItems"
            :key="item.id"
            :id="`blog${item.id}`"
          >
            <img :src="item.image" alt="" data-aos="zoom-in" />
            <div class="d-flex flex-column justify-content-between">
              <div class="titleAndText">
                <h3 class="title">{{ item.title }}</h3>
                <p class="text">{{ item.text }}</p>
              </div>
              <div class="number">0{{ item.id }}.</div>
            </div>
          </div>
          <div
            class="pagination d-flex align-items-center justify-content-center"
          >
            <span
              class="num"
              @click="pagination = 1"
              :class="{ active: pagination == 1 }"
              >01</span
            >
            <span class="whiteLine"></span>
            <span
              class="num"
              @click="pagination = 2"
              :class="{ active: pagination == 2 }"
              >02</span
            >
            <span
              class="num"
              @click="pagination = 3"
              :class="{ active: pagination == 3 }"
              >03</span
            >
            <span
              class="num"
              @click="pagination = 4"
              :class="{ active: pagination == 4 }"
              >04</span
            >
          </div>
        </div>
        <Footer lang="en" />
      </div>
      <div class="faBlogs irancell" v-else>
        <Header lang="fa" @change="change" />
        <div class="topDiv">
          <h3 class="mont">Blog</h3>
          <h1>همه چیز درباره ی آلومینیوم</h1>
          <p>
            لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده
            از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و
            سطرآنچنان که لازم است و برای شرایط فعلی تکنولوژی مورد نیاز.
          </p>
        </div>
        <div class="scroll d-flex justify-content-end align-items-center">
          <div class="scrollIcon">
            <span class="scrollCircle"></span>
          </div>
          <span class="scrollTitle">Scroll Down</span>
        </div>
        <div class="lineDiv">
          <Lines myVw="1920" myVh="360" />
        </div>
        <div class="blogList">
          <div
            class="d-flex justify-content-between blog"
            v-for="(cptpos, index) in cptpost"
            :key="index"
            :id="`blog${cptpos.id}`"
          >
          

            <img :src="cptpos.acf.pimage.url" alt="cptpos.acf.pimage.alt" data-aos="zoom-in" />
            <div class="d-flex flex-column justify-content-between">
              <div class="titleAndText">
                <nuxt-link :to="`/post/${cptpos.id}`">
                  <h3 class="title"> {{ cptpos.acf.ptext}}</h3>  
                </nuxt-link>
  
  <!--               <p class="text" v-html='cptpos.acf.ptextarea'></p>
   -->            </div>
              <div class="number" >0{{cptpos.id}}.</div>
            </div>
  
  
          </div>
          <div
            class="pagination mont d-flex align-items-center justify-content-center"
          >
            <span
              class="num"
              @click="pagination = 1"
              :class="{ active: pagination == 1 }"
              >01</span
            >
            <span class="whiteLine"></span>
            <span
              class="num"
              @click="pagination = 2"
              :class="{ active: pagination == 2 }"
              >02</span
            >
            <span
              class="num"
              @click="pagination = 3"
              :class="{ active: pagination == 3 }"
              >03</span
            >
            <span
              class="num"
              @click="pagination = 4"
              :class="{ active: pagination == 4 }"
              >04</span
            >
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
        pagination: 1,
        blogItems: [
          {
            id: 1,
            image: "/images/homeNew1.jpg",
            title: "Lorem ipsum dolor sit",
            text: `Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt
                  ut labore et dolore magna aliqua Egestas purus viverra accumsan in nisl nisi Arcu cursus
                  vitae congue mauris rhoncus aenean vel elit scelerisque ...`,
          },
  
        ],
        faBlogItems: [
          {
            id: 1,
            image: "/images/homeNew1.jpg",
            title: "لورم ایپسوم متن",
            text: `لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ و با استفاده از طراحان گرافیک است چاپگرها و متون بلکه روزنامه و مجله در ستون و سطرآنچنان که لازم است ...`,
          },
  
        ],
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
            cptpost: []
        }
      },
      async fetch() {
        this.cptpost = await fetch(
          'http://nuxtwp.local/wp-json/acf/v3/cptpost/'
        ).then(res => res.json())
      }
    
    //#
  
  };
  </script>
    
    <style>
  </style>