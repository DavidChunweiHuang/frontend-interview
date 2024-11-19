<template>
  <div class="carousel">
    <swiper
      :modules="[EffectCards, Navigation, Pagination]"
      effect="cards"
      :navigation="true"
      :pagination="{ clickable: true }"
      :grabCursor="true"
      @slideChange="onSlideChange"
      @swiper="onSwiperInit"
    >
      <swiper-slide v-for="(image, index) in images" :key="index">
        <img :src="image" alt="Card Image" />
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import { EffectCards, Navigation, Pagination } from "swiper/modules";
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/scss";
import "swiper/scss/effect-cards";
import "swiper/scss/navigation";
import "swiper/scss/pagination";

export default {
  name: "Carousel",
  props: {
    articles: {
      type: Array,
      required: true,
    },
    activeIndex: {
      type: Number,
      required: true,
    },
  },
  components: {
    Swiper,
    SwiperSlide,
  },
  setup() {
    return {
      EffectCards,
      Navigation,
      Pagination,
    };
  },
  data() {
    return {
      images: [
        "https://picsum.photos/id/12/768/432",
        "https://picsum.photos/id/13/768/432",
        "https://picsum.photos/id/14/768/432",
        "https://picsum.photos/id/15/768/432",
      ],
      swiperInstance: null,
    };
  },
  methods: {
    onSwiperInit(swiper) {
      // Initialize swiper
      this.swiperInstance = swiper;
      console.log("Swiper initialized:", swiper);
    },
    onSlideChange() {
      if (this.swiperInstance) {
        this.$emit("update-index", this.swiperInstance.activeIndex); // 更新 App component currentIndex
      } else {
        console.error("Swiper instance is not available.");
      }
    },
  },
  mounted() {
    this.$nextTick(() => {
      if (this.$refs.swiperRef?.swiper) {
        console.log("Swiper is initialized", this.$refs.swiperRef.swiper);
      } else {
        console.error("Swiper instance is not ready yet.");
      }
    });
  },
};
</script>

<style lang="scss">
@use "../assets/styles/variables.scss" as vars;

.carousel {
  position: relative;
  width: 327px;
  height: 225px;

  z-index: 0;

  @include vars.respond-to(large) {
    width: 1024px;
    height: 432px;
  }

  .swiper {
    width: 100%;
    max-width: 400px;
    height: 225px;

    @include vars.respond-to(large) {
      width: 100%;
      max-width: 726px;
      height: 100%;
    }

    .swiper-slide {
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 18px;
      font-size: 22px;
      font-weight: bold;
      color: #fff;
    }

    .swiper-button-prev,
    .swiper-button-next {
      content: none;

      // 移除 Swiper 的 `:after` 樣式
      &::after {
        color: #fff;
        width: 40px;
        height: 40px;

        border-radius: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
      }

      // 移除 :before
      &::before {
        content: none;
      }
    }

    .swiper-pagination {
      bottom: 10px;
      display: flex;
      justify-content: center;

      .swiper-pagination-bullet {
        width: 32px;
        height: 8px;
        margin: 0 8px;
        border-radius: 4px;
        background-color: rgba(255, 255, 255, 0.5);
        transition: background-color 0.3s ease, transform 0.3s ease;
      }

      .swiper-pagination-bullet-active {
        background-color: #fff;
        transform: scale(1.3);
      }
    }
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
      box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.5);
    }
  }
}
</style>
