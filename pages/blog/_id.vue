<template>
  <div>
    <h2>{{ item.title }}</h2>
    <div v-html="item.body"></div>
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
