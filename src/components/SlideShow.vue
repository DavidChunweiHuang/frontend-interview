<template>
  <div class="carousel">
    <div
      class="carousel-item"
      v-for="(image, index) in images"
      :key="index"
      :class="{ active: currentIndex === index }"
    >
      <img :src="image" alt="Carousel Image" />
    </div>
    <!-- 其他輪播內容或左右切換按鈕 -->
  </div>
</template>

<script>
export default {
  name: "Carousel",
  data() {
    return {
      images: [
        "https://picsum.photos/id/12/768/432",
        "https://picsum.photos/id/13/768/432",
        "https://picsum.photos/id/14/768/432",
      ],
      currentIndex: 0,
    };
  },
  methods: {
    startCarousel() {
      setInterval(() => {
        this.currentIndex = (this.currentIndex + 1) % this.images.length;
      }, 3000); // 每 3 秒切換一次圖片
    },
  },
  mounted() {
    this.startCarousel();
  },
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;

.carousel {
  position: relative;
  width: 327px;
  height: 184px;
  overflow: hidden;

  @include vars.respond-to(large) {
    width: 768px;
    height: 432px;
  }

  .carousel-item {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    opacity: 0;
    transition: opacity 1s ease-in-out;

    &.active {
      opacity: 1;
    }

    img {
      width: 100%;
      border-radius: 10px;
      object-fit: contain;
    }
  }
}
</style>
