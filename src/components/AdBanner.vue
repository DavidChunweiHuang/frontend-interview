<template>
  <div class="ad-banner">
    <div class="ad-placeholder">300 x 250</div>
  </div>
</template>

<script>
export default {
  name: "AdBanner",
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;
.ad-banner {
  display: flex;
  justify-content: center;
  padding: 20px;
}

.ad-placeholder {
  width: 300px;
  height: 250px;
  background-color: #ccc;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;

  @include vars.respond-to(large) {
    width: 970px;
    height: 250px;
  }
}
</style>
