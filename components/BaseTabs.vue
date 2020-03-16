<template>
  <div>
    <div class="tabs">
      <ul>
        <li v-for="(tab, index) in tabs" :key="index" :class="{ 'is-active': tab.isActive }">
          <a :href="tab.href" @click="selectTab(tab)">{{ tab.name }}</a>
        </li>
      </ul>
    </div>

    <div class="tabs-details">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      tabs: []
    }
  },
  created () {
    this.tabs = this.$children
  },
  methods: {
    selectTab (selectedTab) {
      this.tabs.forEach((tab) => {
        tab.isActive = (tab.name === selectedTab.name)
      })
    }
  }
}
</script>

<style lang="scss">
  @import "~/assets/scss/variables";

  .tabs {
    ul {
      width: 100%;
      display: flex;
      list-style: none;
      padding: 0;
      margin: 0;
      border-bottom: 1px solid $border-color-accent;
    }

    li {
      flex-grow: 1;
      text-align: center;

      a {
        display: block;
        color: $text-color-accent;
        text-decoration: none;
        padding: 16px 0;
      }

      &.is-active {
        a {
          color: $text-color-primary;
          font-weight: bold;
          border-bottom: 3px solid $border-color-accent;
        }
      }
    }
  }
</style>
