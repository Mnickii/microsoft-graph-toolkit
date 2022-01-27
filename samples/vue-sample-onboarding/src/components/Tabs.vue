<template>
  <div>
    <div class="tabs-inner-nav">
      <ul class="nav nav-pills">
        <li class="home"
            :class="{ active: active === 'Home'}"
            @click="setActiveTab('Home')">Home</li>
        <li class="reader"
            :class="{ active: active === 'Reader'}"
            @click="setActiveTab('Reader')">Reader</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Tabs',
  data() {
    return {
      active: 'Home',
    };
  },
  methods: {
    setActiveTab(tabName) {
      this.active = tabName;
      this.$emit(`on${tabName}`);
    },
  },
});
</script>

<style lang="scss">
.tabs-inner-nav {
    font-family: 'Circular-Bold', sans-serif;
    display: flex;
    justify-content: center;
    margin-top: 48px;
    a:link, a:visited {
      color: #000;
      font-size: 18px;
    }
    a:hover {
      text-decoration: none;
      padding-bottom: 2px;
      border-bottom: 2px solid #559673;
    }
    li {
      font-size: 18px;
      // margin-left: 72px;
      cursor: pointer;
      &.active {
        border-bottom: 4px solid #559673;
      }
    }
    li:active {
      border-bottom: 4px solid #559673;
    }
  }

  .reader {
    margin-left: 72px;
  }

  .home {
    margin-right: 72px;
  }
</style>
