<template>
  <draggable-item v-bind="$attrs" v-on="$listeners" class="c-draggable-item--small-image"/>
</template>

<script>
  import DraggableItem from './DraggableItem.vue'

  export default {
    name: 'ImageSmall',
    components: {
      DraggableItem
    },
    inheritAttrs: false
  }
</script>

<style lang="scss" scoped>
  .c-draggable-item--small-image {
    // background-color: #526cae;
  }
</style>
