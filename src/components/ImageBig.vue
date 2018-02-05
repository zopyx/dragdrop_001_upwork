<template>
  <draggable-item v-bind="$attrs" v-on="$listeners" class="c-draggable-item--big-image"/>
</template>

<script>
  import DraggableItem from './DraggableItem.vue'

  export default {
    name: 'ImageBig',
    components: {
      DraggableItem
    },
    inheritAttrs: false
  }
</script>

<style lang="scss" scoped>
  .c-draggable-item--big-image {
    // background-color: #579b56;
  }
</style>
