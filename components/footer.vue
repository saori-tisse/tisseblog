<template>
  <footer class="footer l-footer" id="footer">
    <div class="footer-sns">
      <ul class="footer-sns_list">
        <li>
          <a href="https://github.com/saori-tisse/" target="_blank" rel="noopenner">
            <i class="fab fa-github"></i>
          </a>
        </li>
        <li>
          <a href="https://codepen.io/chisaweb" target="_blank" rel="noopenner">
            <i class="fab fa-codepen"></i>
          </a>
        </li>
        <li>
          <a href="https://twitter.com/tisse_web" target="_blank" rel="noopenner">
            <i class="fab fa-twitter"></i>
          </a>
        </li>
        <li>
          <a href="https://www.instagram.com/saori_tissedesign/" target="_blank" rel="noopenner">
            <i class="fab fa-instagram"></i>
          </a>
        </li>
      </ul>
    </div>
    <p class="copyright">
      <small>
        &copy;
        <nuxt-link :to="'/'">tisse design</nuxt-link>
      </small>
    </p>
  </footer>
</template>


<style lang="scss" scoped>
.footer {
  padding: rem(50) 0 rem(20);
  &-sns {
    &_list {
      padding: 0;
      display: flex;
      justify-content: center;
      li {
        font-size: rem(32);
        &:not(:last-child) {
          margin-right: rem(20);
        }
      }
      a {
        color: $color-main;
        &:hover {
          opacity: 0.7;
        }
      }
    }
  }
}
.copyright {
  margin-top: rem(16);
  text-align: center;
  a {
    color: $color-text;
  }
}
</style>
