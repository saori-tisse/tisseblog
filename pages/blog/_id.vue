<template>
  <div class="wrap post-wrap">
    <div>
      <div class="post-meta">
        <div class="thubcatch" v-if="item.icatch">{{item.icatch}}</div>
        <h2>{{ item.title }}</h2>
        <p class="tile">
          <time>{{item.createdAt}}</time>
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
  &-contents {
    h2 {
      margin-top: rem(24);
      font-size: rem(24);
      + * {
        margin-top: rem(12);
      }
    }
    h3 {
      font-size: rem(20);
      + * {
        margin-top: rem(8);
      }
    }
    p {
      + * {
        margin: rem(8);
      }
    }
  }
}
</style>
