<template>
  <div :class="'logo-container-' + layout">
    <router-link to="/">
      <!-- 这里是logo变更的位置 -->
      <!-- <vab-remix-icon v-if="logo" class="logo" :icon-class="logo" /> -->
      <div class="sys_haed-content">
        <img class="logo" :src="systemInfo.sys_logo" alt="" />
        <span
          class="title"
          :class="{ 'hidden-xs-only': layout === 'horizontal' }"
          :title="systemInfo.sys_name"
        >
          {{ systemInfo.sys_name }}
        </span>
      </div>
    </router-link>
  </div>
</template>
<script>
import { mapGetters } from 'vuex';

export default {
  name: 'VabLogo',
  data() {
    return {
      title: this.$baseTitle,
    };
  },
  computed: {
    ...mapGetters({
      logo: 'settings/logo',
      layout: 'settings/layout',
      systemInfo: 'user/getSysInfo',
    }),
  },
};
</script>
<style lang="scss" scoped>
@mixin container {
  position: relative;
  height: $base-top-bar-height;
  overflow: hidden;
  line-height: $base-top-bar-height;
  background: $base-menu-background;
}

@mixin logo {
  display: inline-block;
  width: 28px;
  height: 28px;
  margin-right: 3px;
  color: $base-title-color;
  vertical-align: middle;
}

@mixin title {
  display: inline-block;
  overflow: hidden;
  font-size: 18px;
  line-height: 55px;
  color: $base-title-color;
  text-overflow: ellipsis;
  white-space: nowrap;
  vertical-align: middle;
}

.logo-container-horizontal {
  @include container;

  .logo {
    @include logo;
  }

  .title {
    @include title;
  }
}

.logo-container-vertical {
  @include container;

  height: $base-logo-height;
  line-height: $base-logo-height;
  text-align: center;

  .logo {
    @include logo;
  }

  .title {
    @include title;

    max-width: calc(#{$base-left-menu-width} - 60px);
  }
}
.sys_haed-content {
  &:hover {
    * {
      display: none;
    }
    &::before {
      content: '←前台';
      color: #fff;
      cursor: pointer;
      font-size: 17px;
    }
  }
}
</style>
