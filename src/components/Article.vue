<template>
  <div class="article">
    <div class="tags">
      <span>#不分癌</span>
      <span>#常見治療問題</span>
    </div>
    <div class="upper-area">
      <p class="article-title">
        {{ description }}
      </p>
    </div>

    <div class="bottom-area">
      <a :href="url" target="_blank" class="read-more">立即閱讀</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "Article",
  props: {
    description: {
      type: String,
      required: true,
    },
    url: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;
.article {
  position: relative;
  width: 327px;
  //   height: 126px;
  display: flex;
  flex-direction: column;
  justify-content: center;

  @include vars.respond-to(large) {
    width: 412px;
    // height: 327px;
  }

  .tags {
    color: #b38e5b;
    padding: 5px;
    border-radius: 5px;
    font-size: 14px;
    margin-bottom: 16px;

    span {
      margin-right: 5px;
    }
  }

  .article-title {
    font-size: 28px;
    font-weight: bold;
    line-height: 1.5;
    margin-bottom: 20px;

    @include vars.respond-to(large) {
      font-size: 32px;
    }
  }

  .bottom-area {
    display: flex;
    justify-content: center;
    align-items: center;

    .read-more {
      color: #ff6700;
      border: 1px solid #ff6700;
      padding: 10px 20px;
      border-radius: 20px;
      background: none;
      text-align: center;
      cursor: pointer;

      &:hover {
        color: #fff;
        background-color: #ff6700;
        border: none;
      }
    }
  }
}
</style>
