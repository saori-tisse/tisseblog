<template>
  <div>
    <Header />
    <nuxt />
  </div>
</template>

<style lang="scss">
@include reset;
@include wrap;

.screen-reader-text {
  position: absolute;
  overflow: hidden;
  width: 1px;
  height: 1px;
  clip: rect(1px, 1px, 1px, 1px);
}
</style>

<script>
import Header from "~/components/header";

export default {
  components: {
    Header
  }
};
</script>
