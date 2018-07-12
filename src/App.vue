<template>
  <div id="app">
    <form class="form" action="">
      <label class="form-item" v-for="i in form.fields">
        <div class="form-item-label">{{i.label}}</div>
        <div class="form-item-content">
          <input
          v-if="i.type == 'text'"
          class="form-input form-item-input"
          v-model="i.value"
          >
          <InputChips
          v-if="i.type=='options-search'"
          class="input"
          :options="i.options"

          v-model="i.value"
          />

        </div>
      </label>
    </form>

  </div>
</template>

<script>
import InputChips from './components/InputChips'

let groupMembers = [
  {value: 'kaihe', label:'何凯'},
  {value: 'Ray', label:'唐瑞峰'},
  {value: 'drew', label:'周亚雄'},
  {value: 'felix', label:'赵炳松'},
  {value: 'guixian', label:'叶桂贤'},
  {value: 'itoes', label:'梁雨旸'},
  {value: 'Jacob', label:'郑嘉龙'},
  {value: 'jeff', label:'邹俊辉'},
  {value: 'page', label:'潘伟彬'},
  {value: 'river', label:'刘艳琦'},
  {value: 'siry', label:'张芯蕊'},
  {value: 'summer', label:'罗瑶瑶'},
  {value: 'tristan', label:'刘旭东'},
  {value: 'walker', label:'冷磊'},
  {value: 'wuyi', label:'方武仪'},
  {value: 'xiaow', label:'刘伟'},
]

export default {
  name: 'App',
  components: {
    InputChips
  },
  data() {
    return {
      form: {
        fields: [
          {name: 'title', label: '标题', type: 'text', value: '',},
          {name: 'members', label: '收件人', type: 'options-search', value: [], options: groupMembers},
        ]
      }
    }
  },
  computed: {
    memberNames() {
      let field = _.find(this.form.fields, ['name', 'members'])
      let members = field.value
      let memberNames = []
      members.forEach(i => {
        memberNames.push(i.label)
      })
      return memberNames
    }
  }
}
</script>

<style lang="scss">
body {
  margin: 0;
}
.form {
  &-input {
    border: none;
    outline: none;
    background: none;
    height: 48px;
  }
  &-item {
    padding: 0 1rem;
    height: 56px;
    display: flex;
    align-items: flex-start;
    box-sizing: border-box;
    border-bottom: 1px solid #0001;
    transition: .3s;

    &:focus-within {
      background: hsla(0, 0%, 0%, .05);
      transition: .1s;
    }
    &-label {
      width: 4em;
      margin-right: 1em;
      flex: none;
      margin-top: 16px;
    }
    &-content {
      flex: 1;
    }
    &-input {
      /* border-bottom: 1px solid; */
      flex: 1;
      width: 100%;
      position: relative;
    }
  }
}
.text-desc {
  opacity: .38;
}
</style>
