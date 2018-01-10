<template>
  <div :class="classes"></div>
</template>

<script>
export default {
  name: 'resizer',
  props: {
    splitType: {
      validator(value) {
        return ['vertical', 'horizontal'].indexOf(value) >= 0
      },
      required: true
    },
    className: String
  },
  computed: {
    classes() {
      const classes = ['panel-resizer', this.split, this.className]
      return classes.join(' ')
    }
  }
}
</script>

<style scoped>
.panel-resizer {
  position: absolute;
  opacity: .2;
  z-index: 1;
  box-sizing: border-box;
  background-clip: padding-box;
}
.panel-resizer.horizontal {
  width: 100%;
  height: 10px;
  cursor: row-resize;
  background-color: #000;
}
.panel-resizer.vertical {
  height: 100%;
  width: 10px;
  cursor: col-resize;
  background-color: #000;
}
</style>