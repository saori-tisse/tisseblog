<template>
  <div class="wrap">
    <h2 class="screen-reader-text">ブログ一覧</h2>
    <div v-for="item in items" class="blog-list">
      <div class="blog-list_item">
        <div class="meta">
          <nuxt-link :to="'blog/' + item.id">
            <h3 class="meta_title">{{ item.title }}</h3>
          </nuxt-link>
        </div>
        <nuxt-link :to="'blog/' + item.id">
          <figure v-if="item.icatch != null" class="img">{{item.icatch}}</figure>
          <div v-else class="img noimg">
            <div class="text">{{ item.title }}</div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      items: []
    };
  },
  async asyncData() {
    const { data } = await axios.get(
      "https://tisseblog.microcms.io/api/v1/blog",
      {
        headers: { "X-API-KEY": process.env.API_KEY }
      }
    );
    return {
      items: data.contents
    };
  }
};
</script>

<style lang="scss" scoped>
.blog-list {
  display: flex;
  margin-top: rem(32);
  &_item {
    display: flex;
    flex-direction: column-reverse;
    width: calc(100% / 3 - 20px);
    margin-top: rem(20);
    box-shadow: 1px 1px 4px rgba(#ccc, 0.5);
    &:nth-child(3n) {
      margin-right: rem(20);
    }
    .meta {
      padding: 1em;
      &_title {
        font-size: rem(20);
        color: $color-main;
      }
    }
    .img {
      // width: ;
      width: 100%;
      padding-top: 235px;
      position: relative;
      img {
        position: absolute;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
    .noimg {
      // background:
      background: linear-gradient(45deg, #07005c, #c4e2ff);
      .text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 80%;
        text-align: center;
        color: #fff;
        text-shadow: 1px 1px 3px rgba(#fff, 0.7);
        font-weight: bold;
        font-size: rem(18);
      }
    }
  }
}
</style>
