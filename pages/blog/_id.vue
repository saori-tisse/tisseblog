<template>
  <div class="wrap post-wrap">
    <div>
      <div class="post-meta">
        <div class="thubcatch" v-if="item.icatch">{{item.icatch}}</div>
        <h1>{{ item.title }}</h1>
        <p class="date -create">
          <i class="far fa-calendar"></i>
          <time :datetime="item.createdAt">{{item.createdAt | moment}}</time>
        </p>
        <p class="date -update" v-if="item.updatedAt">
          <i class="fas fa-sync-alt"></i>
          <time :datetime="item.updatedAt">{{item.updatedAt | moment}}</time>
        </p>
      </div>
      <div class="post-contents">
        <div v-html="item.body"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://tisseblog.microcms.io/api/v1/blog/${params.id}`,
      {
        headers: { "X-API-KEY": process.env.API_KEY }
      }
    );
    return {
      item: data
    };
  },
  filters: {
    moment: function(date) {
      return moment(date).format("YYYY/MM/DD HH:mm");
    }
  }
};
</script>

<style lang="scss" scoped>
.wrap {
  width: 900px;
}
.post {
  &-wrap {
    margin-top: 30px;
  }
  &-meta {
    .date {
      display: inline-block;
      color: #707070;
      margin-right: rem(10);
    }
  }
  &-contents {
    margin-top: rem(50);
    line-height: 1.75;
    /deep/ h2 {
      margin-top: rem(24);
      font-size: rem(24);
      + * {
        margin-top: rem(12);
      }
    }
    /deep/ h3 {
      font-size: rem(20);
      margin-top: rem(12);
      + * {
        margin-top: rem(8);
      }
    }
    /deep/ p {
      + p {
        margin-top: rem(8);
      }
    }
    /deep/ ul {
      margin-top: rem(12);
      padding: 0;
      li {
        position: relative;
        padding-left: rem(30);
        line-height: 2.5;
        &::before {
          content: "\f0a4";
          font-family: "Font Awesome 5 Free";
          display: block;
          position: absolute;
          font-weight: 400;
          font-size: 1.2em;
          top: -3px;
          left: 0;
        }
      }
    }
  }
}
</style>
