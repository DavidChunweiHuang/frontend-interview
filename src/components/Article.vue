<template>
  <div class="article">
    <div class="tags">
      <span>#不分癌</span>
      <span>#常見治療問題</span>
    </div>
    <div class="upper-area">
      <p class="article-title">
        疫情期間，癌症化療病人尿不出來又怕掛急診染疫，怎麼辦？
      </p>
    </div>

    <div class="bottom-area">
      <button class="read-more">立即閱讀</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Article",
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;
.article {
  position: relative;
  width: 327px;
  height: 126px;

  @include vars.respond-to(large) {
    width: 412px;
    height: 327px;
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
