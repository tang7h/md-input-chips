<template>
  <div class="input-chips">
    <div class="selections">

      <div class="chips">
        <chip
        v-for="i in selections"
        :key="i.label"
        :content="i.label"
        @remove="clear"
        ></chip>
      </div>

      <div class="form-item-input">
        <input class="form-input" type="text" v-model="keyword" @keydown.delete="handleKeyboardDelete">

        <div class="suggestion">
          <div class="list-item" v-for="i in suggestions" @click="pick(i)">
            <span class="list-item-title">{{i.label}}</span>
            <span class="list-item-desc">{{i.value}}</span>
          </div>
        </div>

      </div>

    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import Chip from '@/components/Chip'
export default {
  components: {Chip},
  props: ['options', 'value'],
  data() {
    return {
      keyword: '',
      selections: [],
    }
  },
  watch: {
    selections(newValue) {
      this.$emit('input', newValue)
    }
  },
  computed: {
    selectableSelections() {
      return _.difference(this.options, this.selections)
    },
    suggestions() {
      let keyword = this.keyword.toLowerCase()
      if (!keyword) {
        return []
      }
      return _.filter(this.selectableSelections, i => {
        return i.value.toLowerCase().includes(keyword) || i.label.toLowerCase().includes(keyword)
      })
    }
  },
  methods: {
    pick(item) {
      this.selections.push(item)
      this.keyword = ''
    },
    clear(e) {
      this.selections = _.reject(this.selections, ['label', e])
    },
    handleKeyboardDelete() {
      if (!this.keyword && this.selections.length) {
        this.selections.pop()
      }
    }
  }
}
</script>

<style lang="scss">
.selections {
  display: flex;
  align-items: center;
}
.chips {
  display: flex;
  overflow-x: scroll;
}
.chip {
  flex: none;
  color: #232f34;
  background: rgba(#232f34, .12);
  font-size: 14px;
  height: 32px;
  display: flex;
  align-items: center;
  border-radius: 16px;
  padding: 8px;
  box-sizing: border-box;
  margin-right: 8px;
  &-cancel {
    margin-left: 8px;
  }

}
.input-chips {
  position: relative;
}
.suggestion {
  position: absolute;
  top: 100%;
  left: 0;
  background: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,.2);
  border-radius: 4px;
  padding: 8px 0;
}
.list-item {
  height: 40px;
  padding: 0 1em;
  display: flex;
  align-items: center;
  justify-content: space-between;
  &:hover {
    background: #0001;
  }
  &-desc {
    margin-left: 1em;
    opacity: .38;
  }
}
</style>
