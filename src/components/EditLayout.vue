<template>
  <div class="c-edit-layout l-grid l-grid--base" :class="{'is-edit':editable}">
    <div class="l-grid__item l-grid__item--main">
      <div class="c-edit-layout__heading c-heading c-heading--large">#main</div>
      <div class="c-edit-layout__text">
        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Corporis enim eos ipsa magni repudiandae
        sapiente similique voluptatem? Accusantium corporis delectus dolorem eveniet exercitationem minus, modi
        nesciunt! Atque beatae enim ex labore odio omnis quasi quos sed sint temporibus? Ad assumenda, at distinctio
        harum ipsum molestiae obcaecati soluta. Asperiores commodi dignissimos dolor doloremque illo iusto, magni
        omnis qui quos repellendus. Beatae commodi culpa dignissimos distinctio dolorum ducimus earum eius enim et
        facere fugiat, impedit, maiores maxime modi neque nesciunt nobis non officiis quibusdam quo repellat sunt
        tempore tenetur velit vitae voluptate voluptatem, voluptates. Architecto eligendi excepturi exercitationem
        molestias rem repellendus voluptatibus. Ab ad cum excepturi facilis, fuga ipsam labore nam nemo non quod
        repellat tempore vel!
      </div>
    </div>
    <draggable-panel-small-images ref="slot1" :items="slot1" :editable="editable" title="slot1" :group="{name: 'images'}" max-items-count="4"
                                  class="l-grid__item l-grid__item--slot1 c-edit-content__container c-edit-content__container--vertical"/>
    <draggable-panel-big-images ref="slot2" :items="slot2" :editable="editable" title="slot2" :group="{name: 'images'}" max-items-count="6"
                                class="l-grid__item l-grid__item--slot2 c-edit-content__container c-edit-content__container--horizontal"/>
    <draggable-panel v-if="editable" noRemovableItems :editable="editable" title="assets" :items="assets" :group="{name: 'images', 'pull': 'clone', put: false}"
                     class="l-grid__item l-grid__item--assets c-edit-content__container c-edit-content__container--vertical"/>
    <div class="l-grid__item l-grid__item--additional">
      <slot/>
    </div>
  </div>
</template>

<script>
  import DraggablePanel from './DraggablePanel.vue'
  import DraggablePanelBigImages from './DraggablePanelBigImages.vue'
  import DraggablePanelSmallImages from './DraggablePanelSmallImages.vue'

  export default {
    components: {
      DraggablePanelSmallImages,
      DraggablePanelBigImages,
      DraggablePanel},
    name: 'EditContent',
    props: {
      editable: {
        type: Boolean
      },
      assets: {
        type: Array
      },
      slot1: {
        type: Array
      },
      slot2: {
        type: Array
      }
    }
  }
</script>

<style lang="scss" scoped>
  .c-edit-layout {
    //
  }

  .c-edit-layout__heading {
    margin-bottom: rem(10);
  }

  .c-edit-layout__text {
    line-height: 1.4;
    font-size: rem(16);
    font-weight: 400;
  }

  .c-edit-layout.is-edit {
    //
  }

  .c-edit-content__container {
    @include padding(rem(15));
    border: 2px dashed transparent;
    border-radius: rem(5);
  }

  .c-edit-layout.is-edit .c-edit-content__container--draggable {
    border-color: rgba(0, 0, 25, 0.1);
  }

  .c-edit-content__container--large-images {
    min-height: rem(200);
  }

  .l-grid__item--additional {
    border-color: transparent !important;
  }
</style>
