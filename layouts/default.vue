<template>
  <div class="app">
    <aside class="app__menu">
      <div class="app__logo">
        <nuxt-link to="/">
          <img src="http://via.placeholder.com/50/E62202/FFF" alt="logo">
        </nuxt-link>
      </div>
      <ul>
        <li>
          <nuxt-link to="/polls">
            Опросы
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/users">
            Пользователи
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/blacklists">
            Черные списки
          </nuxt-link>
        </li>
        <li>
          <nuxt-link to="/callcenter">
            Колл-центр
          </nuxt-link>
        </li>
      </ul>
    </aside>
    <div class="app__body">
      <header class="app__header">
        <form class="app__searchform" @submit.prevent="submitSearch">
          <input type="search" placeholder="Поиск по системе">
          <button type="submit">
            поиск
          </button>
        </form>
        <div class="app__profile">
          <div class="app__avatar">
            <img src="http://placehold.it/48x48" alt="">
          </div>
          <div>
            <div class="app__username">
              Alexander C.
            </div>
            <div class="app__role">
              Администратор
            </div>
          </div>
        </div>
      </header>
      <section class="app__page">
        <nuxt />
      </section>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      search: ''
    }
  },
  methods: {
    submitSearch () {
      // eslint-disable-next-line no-console
      console.log(this.search)
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/variables";

.app {
  display: flex;
  height: 100vh;

  &__logo {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    overflow: hidden;
  }

  &__menu {
    width: 200px;
    border-right: 1px solid $border-color-default;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 16px;

    ul {
      padding: 0;
      margin: 0;
      list-style: none;
      margin-top: 64px;
      width: 100%;

      a {
        display: flex;
        width: 100%;
        height: 100px;
        align-items: center;
        justify-content: center;
        text-decoration: none;
        color: $text-color-primary;
        border: 1px solid transparent;
        border-radius: 5px;
        margin-bottom: 16px;

        &:hover {
          border-color: $border-color-accent;
          color: $text-color-accent;
        }

        &.nuxt-link-active {
          font-weight: bold;
          background: $background-color-accent;
        }
      }
    }
  }

  &__body {
    flex-grow: 1;
    padding: 32px;
    overflow: auto;
  }

  &__header {
    display: flex;
    justify-content: space-between;
  }

  &__profile {
    display: flex;
    align-items: center;
  }

  &__username {
    font-weight: bold;
  }

  &__role {
    color: $text-color-secondary;
  }

  &__avatar {
    margin-right: 16px;
    overflow: hidden;
    width: 48px;
    height: 48px;
    border-radius: 50%;
  }
}
</style>
