<template>
  <div class="wrap">
    <h2 class="screen-reader-text">ブログ一覧</h2>
    <div v-for="item in items" class="blog-list">
      <div class="blog-list_item">
        <div class="meta">
          <nuxt-link :to="'blog/' + item.id">
            <h3 class="meta_title">{{ item.title }}</h3>
          </nuxt-link>
          <p class="meta_time">
            <time :datetime="item.createdAt">
              <i class="far fa-calendar"></i>
              {{item.createdAt | moment }}
            </time>
          </p>
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
import moment from "moment";

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
  },
  filters: {
    moment: function(date) {
      return moment(date).format("YYYY/MM/DD");
    }
  }
};
</script>

<style lang="scss" scoped>
.blog-list {
  display: flex;
  flex-wrap: wrap;
  margin-top: rem(32);
  &_item {
    display: flex;
    flex-direction: column-reverse;
    width: calc(100% / 3 - 20px);
    margin-top: rem(20);
    box-shadow: 1px 1px 4px rgba(#ccc, 0.5);
    transition: box-shadow 0.3s ease-in-out;
    @include mqdown(tab) {
      width: calc(50% - 20px);
    }
    @include mqdown(sp) {
      width: 100%;
    }
    &:hover {
      box-shadow: 2px 2px 4px rgba(#ccc, 0.7);
    }
    &:nth-child(3n) {
      margin-right: rem(20);
      @include mqdown(tab) {
        margin-right: 0;
      }
    }
    &:nth-child(2n) {
      @include mqdown(tab) {
        margin-right: rem(20);
      }
      @include mqdown(sp) {
        margin-right: 0;
      }
    }
    .meta {
      padding: 1em;
      &_title {
        font-size: rem(18);
        color: $color-main;
        min-height: rem(60);
        @include mqdown(sp) {
          font-size: rem(16);
        }
      }
      &_time {
        font-size: rem(16);
        color: #707070;
        @include mqdown(sp) {
          font-size: rem(12);
        }
      }
    }
    .img {
      // width: ;
      width: 100%;
      padding-top: 235px;
      position: relative;
      overflow: hidden;
      img {
        position: absolute;
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform 0.4s ease-in-out;
        transform-origin: center;
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
