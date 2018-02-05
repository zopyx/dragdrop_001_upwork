<template>
  <draggable-panel v-bind="$attrs" check="smallImage" class="c-draggable-panel--small-images"/>
</template>

<script>
  import DraggablePanel from './DraggablePanel.vue'
  import DraggablePanelMixin from './DraggablePanelMixin.js'

  export default {
    name: 'DraggablePanelSmallImages',
    // extends: DraggablePanelMixin,
    components: {
      DraggablePanel
    },
    inheritAttrs: false,
    methods: DraggablePanelMixin
  }
</script>

<style lang="scss" scoped>
  .c-draggable-panel--small-images {
    //
  }
</style>
