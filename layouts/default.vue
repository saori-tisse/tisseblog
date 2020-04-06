<template>
  <div>
    <Header />
    <nuxt />
    <Footer />
  </div>
</template>

<style lang="scss">
@include reset;
@include wrap;

// component
.sec_ttl {
  text-align: center;
  font-size: rem(32);
  @include ls(100);
  font-family: $Great;
  span {
    background: linear-gradient(transparent 50%, #e6eaff 50%);
  }
  + * {
    margin-top: rem(40);
  }
}
.sub_ttl {
  font-size: rem(20);
  text-align: center;
  + * {
    margin-top: rem(20);
  }
}

.flex {
  display: flex;
}

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
import Footer from "~/components/footer";

export default {
  components: {
    Header,
    Footer
  }
};
</script>
