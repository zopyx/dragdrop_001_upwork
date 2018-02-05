<template>
  <div class="c-draggable-panel" :class="{'is-editable':editable}">
    <div class="c-draggable-panel__heading c-heading c-heading--large">#{{ title
      }}
    </div>
    <draggable class="c-draggable-panel__body" v-model="collection"
               :options="{group, draggable:'.c-draggable-item', ghostClass: 'c-draggable-item--ghost'}"
               :move="checkMove" @end="endDrag" @start="startDrag">
      <component :is="item.type" :removable="!noRemovableItems" :item="item" v-for="(item, index) in collection" :key="item.id" @remove="removeItem(index)"/>
    </draggable>
  </div>
</template>

<script>
  import draggable from 'vuedraggable'
  import DraggableItem from './DraggableItem'
  import bigImage from './ImageBig.vue'
  import smallImage from './ImageSmall.vue'

  export default {
    name: 'DraggablePanel',
    components: {
      smallImage,
      bigImage,
      DraggableItem,
      draggable
    },
    props: {
      title: {
        required: true,
        type: String
      },
      editable: {
        type: Boolean
      },
      items: {
        type: Array,
        default: () => {
          return []
        }
      },
      check: {
        type: String
      },
      group: {
        type: Object
      },
      maxItemsCount: {
        type: [Number, String]
      },
      noRemovableItems: {
        type: Boolean
      }
    },
    data () {
      return {
        collection: this.items || [],
        dragging: false,
        targetElement: null,
        canDrag: null,
        futureIndex: null
      }
    },
    methods: {
      privateCheckMove: function (evt) {
        this.targetElement = evt.relatedContext.element
        if (evt.relatedContext.component.$el === evt.from) {
          return true
        }
        if (evt.relatedContext.component.$options.parent.maxItemsCount && evt.relatedContext.component.$options.parent.maxItemsCount <= evt.relatedContext.list.length) {
          return false
        }
        if (evt.relatedContext.component.$options.parent.check && evt.draggedContext.element.type !== evt.relatedContext.component.$options.parent.check) {
          return false
        }
        return true
      },
      checkMove: function (evt) {
        const res = this.privateCheckMove(evt)
        this.canDrag = res
        this.futureIndex = evt.draggedContext.futureIndex
        return res
      },
      endDrag: function () {
        this.canDrag = null
        this.targetElement = null
        this.futureIndex = null
      },
      startDrag: function (evt) {
        //
      },
      removeItem (index) {
        this.collection.splice(index, 1)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .c-draggable-panel {
    position: relative;
    border: 2px solid rgba(0, 0, 25, 0.04);
  }

  .c-draggable-panel.is-editable {
    border-color: rgba(0, 0, 25, 0.1);
    border-radius: rem(5);
    border-style: dashed;
  }

  .c-draggable-panel__heading {
    @include position(absolute, rem(2) rem(15) null);
    @include padding(rem(13) null rem(15));
    height: rem(59);
    z-index: 99;
    background-color: #f2f3f7;

    .c-popup-edit-layout & {
      background-color: white;
    }
  }

  .c-draggable-panel__body {
    overflow-y: auto;
    @include padding(rem(34 + 15 * 2) rem(15) rem(15));
    @include position(absolute, 0);
  }
</style>
