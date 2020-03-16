<template>
  <div class="polls">
    <base-tabs>
      <base-tab name="Параметры" :selected="true">
        <div class="polls__tab">
          Параметры
        </div>
      </base-tab>
      <base-tab name="Вопросы">
        <div class="polls__tab">
          Вопросы
        </div>
      </base-tab>
      <base-tab name="Логика">
        <div class="polls__tab">
          Логика
        </div>
      </base-tab>
      <base-tab name="Условия">
        <div class="polls__tab">
          Условия
        </div>
      </base-tab>
      <base-tab name="Респонденты">
        <poll-respondents :rules="poll.respondents" />
      </base-tab>
    </base-tabs>
    <div class="polls__buttons">
      <button class="polls__button" @click="logPoll">
        Протестировать опрос
      </button>
      <button class="polls__button" @click="logPoll">
        Далее →
      </button>
    </div>
  </div>
</template>

<script>
import BaseTabs from '../components/BaseTabs'
import BaseTab from '../components/BaseTab'
import PollRespondents from '../components/PollRespondents'

export default {
  components: {
    PollRespondents,
    BaseTabs,
    BaseTab
  },
  data () {
    return {
      poll: {
        respondents: []
      }
    }
  },
  methods: {
    logPoll () {
      // eslint-disable-next-line no-console
      console.log(this.poll)
    }
  }
}
</script>

<style lang="scss">
  @import "~/assets/scss/variables";

  .polls {
    &__tab {
      padding: 15px;
    }
    &__buttons {
      padding: 16px;
      display: flex;
      justify-content: space-between;
    }
    &__button {
      background: #FFF;
      border: 1px solid $border-color-accent;
      color: $text-color-accent;
      padding: 16px;
      cursor: pointer;
      border-radius: 5px;
    }
  }
</style>
