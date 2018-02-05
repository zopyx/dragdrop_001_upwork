<template>
  <div class="c-draggable-item" :style="item.style">
    <div class="c-draggable-item__close" @click="$emit('remove')" v-if="removable">
      <close-icon/>
    </div>
  </div>
</template>

<script>
  import CloseIcon from './CloseIcon.vue'

  export default {
    components: { CloseIcon },
    name: 'DraggableItem',
    props: {
      item: {
        type: Object,
        required: true
      },
      removable: {
        type: Boolean
      },
      type: {
        type: String
      }
    }
  }
</script>

<style lang="scss" scoped>
  .c-draggable-item {
    position: relative;
    width: 100%;
    float: left;
    overflow: hidden;
    max-width: susy-span(4 of $g-grid-columns-count);
    border-radius: rem(5);
    background-repeat: no-repeat;
    background-position: center center;
    cursor: move;
    margin-top: rem($g-indent-small);

    &:hover {
      background-color: rgba(0, 0, 25, 0.05);
    }

    &::before {
      content: '';
      display: block;
      padding-top: 100%;
    }

    .c-edit-content__container--vertical & {
      max-width: 100%;
    }

    .c-edit-content__container--horizontal & {
      //
    }
  }

  .c-draggable-item--ghost {
    opacity: 0.25;
  }

  .c-draggable-item__close {
    $width: rem(24);
    @include position(absolute, 0 0 null null);
    //@include margin((-$width / 2) (-$width / 2) null null);
    width: $width;
    height: $width;
    line-height: $width;
    //border-radius: 50%;
    //background-color: white;
    opacity: 0;
    text-align: center;
    cursor: pointer;

    .c-draggable-item:hover & {
      opacity: 1;
    }
  }

  .c-draggable-item__close svg {
    display: inline-block;
    $width: rem(12);
    width: $width;
    height: $width;
    fill: #333;
  }
</style>
