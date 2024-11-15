<!-- src/App.vue -->
<template>
  <div class="app" ref="appContainer">
    <AdBanner />
    <Header :isNavbarVisible="isNavbarVisible" />
    <div class="content">
      <Article v-if="isLargeScreen" />
      <Carousel />
      <Article v-if="!isLargeScreen" />
    </div>
    <Content />
  </div>
</template>

<script>
import AdBanner from "./components/AdBanner.vue";
import Header from "./components/Header.vue";
import Carousel from "./components/SlideShow.vue";
import Article from "./components/Article.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    AdBanner,
    Header,
    Carousel,
    Article,
    Content,
  },
  data() {
    return {
      isNavbarVisible: true,
      lastScrollTop: 0,
      isLargeScreen: window.innerWidth >= 1440,
    };
  },
  methods: {
    handleResize() {
      // 當螢幕尺寸改變時更新 isLargeScreen
      this.isLargeScreen = window.innerWidth >= 1440;
    },
    handleScroll() {
      const scrollTop = this.$refs.appContainer.scrollTop; // window.pageYOffset || document.documentElement.scrollTop;

      if (scrollTop > this.lastScrollTop) {
        // 向下滾動，隱藏 Navbar，顯示 Search Bar
        this.isNavbarVisible = false;
      } else {
        // 向上滾動，顯示 Navbar
        this.isNavbarVisible = true;
      }
      this.lastScrollTop = scrollTop <= 0 ? 0 : scrollTop; // 確保不會小於 0
    },
  },
  mounted() {
    // window.addEventListener("scroll", this.handleScroll);
    this.$refs.appContainer.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    // window.removeEventListener("scroll", this.handleScroll);
    this.$refs.appContainer.removeEventListener("scroll", this.handleScroll);
  },
};
</script>

<style lang="scss">
@use "./assets/styles/variables.scss" as vars;
.app {
  // position: relative;
  // max-width: 375px;
  height: 860px;
  margin: 0 auto;
  background-color: #fff;
  color: #333;
  overflow-y: auto;
  padding: 0 30px;

  @include vars.respond-to(large) {
    max-width: 1440px;
    height: auto;
  }

  .content {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    gap: 20px;

    @include vars.respond-to(large) {
      margin-top: 64px;
      flex-direction: row;
      justify-content: space-between;
      align-items: end;
      gap: 45px;
    }
  }
}
</style>
