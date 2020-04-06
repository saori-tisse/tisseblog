<template>
  <header class="header l-header" id="header">
    <div class="wrap">
      <nav class="globalnav">
        <ul class="globalnav_list">
          <li>
            <nuxt-link :to="'/about/'">Profile</nuxt-link>
          </li>
          <li>
            <nuxt-link :to="'/'">Blog</nuxt-link>
          </li>
          <li>
            <a href="http://tisse-design.com/contact/">Contact</a>
          </li>
        </ul>
      </nav>
    </div>
  </header>
</template>

<style lang="scss" scoped>
.header {
  // background: #07005c;
}
.globalnav {
  &_list {
    // color: #ffffff;
    color: $color-main;
    display: flex;
    justify-content: flex-end;
    li {
      &:not(:last-child) {
        margin-right: rem(20);
      }
    }
    a {
      color: $color-main;
      display: block;
      padding: rem(16) 0;
      text-transform: uppercase;
    }
  }
}
</style>
