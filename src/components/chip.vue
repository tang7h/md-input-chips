<template>
  <div class="chip">
    <div class="chip-content">{{content}}</div>
    <IconCancel class="chip-cancel" @click.native="remove"/>
  </div>
</template>
<script>
import IconCancel from '@/components/IconCancel'

export default {
  props: ['content'],
  data() {
    return {
    }
  },
  components: {IconCancel},
  methods: {
    remove() {
      this.$emit('remove', this.content)
    }
  }
}
</script>
