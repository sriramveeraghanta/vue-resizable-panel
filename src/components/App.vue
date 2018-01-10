<template>
  <div :class="classes" @mousemove="onMouseMove" @mouseup="onMouseUp">
    
    <Panel :splitType="splitType">
      <slot name="panel-left"></slot>
      <div>
        Panel Left
      </div>
    </Panel>

    <Resizer :splitType="splitType" />

    <Panel :splitType="splitType">
      <slot name="panel-right"></slot>
      <div>
        Panel Right
      </div>
    </Panel>
  
  </div>
</template>

<script>
export default {
  name: 'app',

  props: {
    minPercent: {
      type: Number,
      default: 10
    },
    defaultPercent: {
      type: Number,
      default: 50
    },
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
      const classes = ['split-panel-container', this.split, this.className]
      return classes.join(' ')
    }
  },
  data() {
    return {
      active: false,
      hasMoved: false,
      split: 50,
    }
  },
  methods: {
    onMouseDown(e) {
      this.dragging = true
      this.startX = e.pageX
      this.startSplit = this.split
    },
    onMouseMove(e){
      if(this.dragging) {
        const dx = e.pageX - this.startX
        const totalWidth = this.$el.offsetWidth
        this.split = this.startSplit + ~~(dx / totalWidth * 100)
      }
    },
    onMouseUp(e){
      this.dragging = false
    }
  }
}
</script>

<style scoped>
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
.split-panel-container {
  height: 100%;
  position: relative;
  display: flex;
}
.split-panel-container.vertical {
  flex-direction: row;
}
.split-panel-container.horizontal {
  flex-direction: column;
}

</style>