<template>
  <draggable-panel v-bind="$attrs" check="bigImage" class="c-draggable-panel--big-images"/>
</template>

<script>
  import DraggablePanel from './DraggablePanel.vue'
  import DraggablePanelMixin from './DraggablePanelMixin.js'

  export default {
    name: 'DraggablePanelBigImages',
    components: {
      DraggablePanel
    },
    inheritAttrs: false,
    methods: DraggablePanelMixin
  }
</script>

<style lang="scss" scoped>
  .c-draggable-panel--big-images {
    //min-height: rem(400);
  }
</style>
