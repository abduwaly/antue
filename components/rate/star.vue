<template>
  <li :class="getClassName()" @click="onClickHandler" @mousemove="onHoverHandler">
    <div :class="`${this.prefixCls}-first`"><slot></slot></div>
    <div :class="`${this.prefixCls}-second`"><slot></slot></div>
  </li>
</template>

<script>
export default {
  name: 'star',
  props: {
    newValue: Number,
    index: Number,
    prefixCls: String,
    allowHalf: Boolean,
    disabled: Boolean
  },
  data () {
    return {
    }
  },
  methods: {
    onHoverHandler (e) {
      if (this.disabled) return
      this.$emit('hover', e, this.index)
    },
    onClickHandler (e) {
      if (this.disabled) return
      this.$emit('click', e, this.index)
    },
    getClassName () {
      const starValue = this.index
      if (this.allowHalf && this.newValue + 0.5 === starValue) {
        return `${this.prefixCls} ${this.prefixCls}-half ${this.prefixCls}-active`
      }
      if (starValue <= this.newValue) {
        return `${this.prefixCls} ${this.prefixCls}-full`
      } else {
        return `${this.prefixCls} ${this.prefixCls}-zero`
      }
    }
  }
}
</script>
