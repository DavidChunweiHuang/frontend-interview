<template>
  <div class="content"></div>
</template>

<script>
export default {
  name: "Content",
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;

.content {
  background-color: #ffffff;
  width: 328px;
  height: 234px;

  @include vars.respond-to(large) {
    width: 1024px;
    height: 500px;
  }
}
</style>