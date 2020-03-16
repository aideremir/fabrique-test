<template>
  <div class="poll-respondents">
    <div class="poll-respondents__header">
      Добавить опрос
    </div>
    <div class="poll-respondents__rules">
      <div v-for="(rule, index) in rules" :key="index" class="poll-respondents__rule">
        <div class="poll-respondents__row">
          <div class="poll-respondents__col poll-respondents__col--label">
            Условие {{ index + 1 }}
          </div>
          <div class="poll-respondents__col">
            <select v-model="rule.type">
              <option value="">
                Выберите условие
              </option>
              <option v-for="(ruleType, type) in ruleTypes" :key="type" :value="type">
                {{ ruleType.name }}
              </option>
            </select>
          </div>
        </div>
        <template v-if="rule.type">
          <div v-for="(arg, argIndex) in rule.arguments" :key="argIndex" class="poll-respondents__row">
            <div class="poll-respondents__col poll-respondents__col--label">
              <span v-if="argIndex" class="poll-respondents__logic">или</span>
              {{ ruleTypes[rule.type].entityName }} {{ argIndex + 1 }}
            </div>
            <div class="poll-respondents__col">
              <template v-if="rule.type === 'age'">
                от <input v-model="arg.from" type="number"> до <input v-model="arg.to" type="number">
              </template>
              <template v-else>
                <select v-model="arg.value">
                  <option
                    v-for="(option, optindex) in ruleTypes[rule.type].options"
                    :key="optindex"
                    :value="option.value"
                  >
                    {{ option.label }}
                  </option>
                </select>
              </template>
              <button class="poll-respondents__button poll-respondents__button--delete" @click="deleteArgument(rule.arguments, arg)">
                &times;
              </button>
            </div>
          </div>
        </template>
        <div class="poll-respondents__row">
          <div class="poll-respondents__col poll-respondents__col--label" />
          <div class="poll-respondents__col poll-respondents__col--buttons">
            <button class="poll-respondents__button poll-respondents__button--delete" @click="deleteRule(rule)">
              Удалить условие
            </button>
            <button v-if="rule.type" class="poll-respondents__button" @click="addRuleArgument(rule)">
              Добавить {{ ruleTypes[rule.type].entityName }}
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="poll-respondents__add">
      <button @click="addRule">
        &plus;<br>
        Нажмите, чтобы добавить новое условие выборки.<br>
        Все условия связываются между собой логическим «И»
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PollRespondents',
  props: {
    rules: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      ruleTypes: {
        age: {
          name: 'Возраст респондента',
          entityName: 'диапазон'
        },
        cardType: {
          name: 'Тип карты лояльности',
          entityName: 'тип',
          options: [
            { value: 'silver', label: 'Silver' },
            { value: 'gold', label: 'Gold' },
            { value: 'platinum', label: 'Platinum' }
          ]
        },
        cardStatus: {
          name: 'Статус карты лояльности',
          entityName: 'статус',
          options: [
            { value: 'active', label: 'Активна' },
            { value: 'inactive', label: 'Не активна' }
          ]
        }
      }
    }
  },
  methods: {
    addRule () {
      this.rules.push({
        type: '',
        arguments: []
      })
    },
    addRuleArgument (rule) {
      const argument = rule.type === 'age' ? {
        from: '',
        to: ''
      } : {
        value: this.ruleTypes[rule.type].options[0].value
      }
      rule.arguments.push(argument)
    },
    deleteRule (rule) {
      this.$delete(this.rules, this.rules.indexOf(rule))
    },
    deleteArgument (args, argument) {
      this.$delete(args, args.indexOf(argument))
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/variables";

.poll-respondents {
  &__header {
    padding: 16px;
    color: $text-color-secondary;
    font-weight: bold;
  }
  &__rule {
    padding: 16px;
    &:nth-child(odd) {
      background: #fffcf6;
    }
    &:nth-child(even) {
      background: #f8faff;
    }
    border-bottom: 1px solid $border-color-default;
  }
  &__row {
    display: flex;
    margin-bottom: 16px;
  }
  &__col {
    &:last-child {
      flex-grow: 1;
    }
    &--label {
      width: 25%;
      text-transform: capitalize;
    }

    &--buttons {
      display: flex;
      flex-direction: row-reverse;
      justify-content: space-between;
    }

    input {
      width: 100px;
    }
  }
  &__logic {
    display: inline-block;
    text-transform: lowercase;
    color: $text-color-secondary;
  }
  &__button {
    border: 1px solid $border-color-accent;
    cursor: pointer;
    color: $text-color-accent;
    border-radius: 5px;

    &--delete {
      color: $text-color-danger;
      border-color: $border-color-danger;
    }
  }
  &__add {
    padding: 16px;
    button {
      width: 100%;
      border: 1px solid $border-color-accent;
      border-radius: 5px;
      padding: 16px 0;
      cursor: pointer;
      color: $text-color-accent;
    }
  }
}
</style>
