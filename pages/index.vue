<template>
  <div>
    <div class="top_mv">
      <img src="~/assets/img/bg_mv.jpg" alt v-parallax="0.5" />
    </div>
    <div class="wrap">
      <section class="top_sec top-service">
        <h2 class="sec_ttl">
          <span>Service</span>
        </h2>
        <ul class="top-service_list flex">
          <li>
            <div class="top-service_item">
              <div class="textbox">
                <h3 class="sub_ttl">Webサイト制作</h3>
                <p class="desp">企画からデザイン、コーディングまで一貫して対応いたします。</p>
              </div>
            </div>
          </li>
          <li>
            <div class="top-service_item">
              <div class="textbox">
                <h3 class="sub_ttl">コーディング代行</h3>
                <p class="desp">HTML/CSS、JavaScript、WordPressなどのコーディング代行を承っています。</p>
              </div>
            </div>
          </li>
        </ul>
      </section>
      <!-- /.top-service -->
      <section class="top_sec top-blog">
        <h2 class="sec_ttl">
          <span>Blog</span>
        </h2>
        <div class="blog-list">
          <div v-for="item in items" class="blog-list_item">
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
      </section>
      <section class="top-profile">
        <h2 class="sec_ttl">
          <span>Profile</span>
        </h2>

        <div class="top-profile_img">
          <img src="~/assets/img/img_prof.jpg" alt />
        </div>
        <div class="top-profile_text">
          <h3 class="name">なかみち さおり</h3>
          <p>
            1990年10月生まれ
            <br />医療機器のCEやインフラ営業企画・技術支援を経験。
            <br />家族の転勤のため退職し、家でも働けるスキルを、Webデザイナーを目指す。
            <br />現在は、フリーランスのコーダーとして活動中。
          </p>
          <dl>
            <dt>スキル</dt>
            <dd>HTML / CSS / JavaScript (jQuery,Vanilla) / PHP / WordPress</dd>
          </dl>
        </div>
      </section>
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
.top {
  &_sec {
    + * {
      margin-top: rem(100);
    }
  }
  &_mv {
    height: 500px;
    overflow: hidden;
    + * {
      margin-top: rem(60);
    }
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
    }
  }
  &-service {
    &_list {
      justify-content: space-between;
      li {
        width: calc(100% / 2 - 32px);
      }
    }
    &_item {
      border-radius: 4px;
      box-shadow: 0 0 4px 0px rgba($color-main, 0.25);
      padding: 1em;
    }
  }
  &-profile {
    &_img {
      width: 120px;
      margin-right: auto;
      margin-left: auto;
      border-radius: 50%;
      overflow: hidden;
    }
    &_text {
      width: 600px;
      max-width: 100%;
      margin: rem(30) auto;
      .name {
        text-align: center;
        font-weight: normal;
        @include ls(50);
      }
    }
  }
}
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
    &:not(:nth-child(3n)) {
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
