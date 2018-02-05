<template>
  <div class="c-popup-edit-layout" :class="{'is-active':isActive}">
    <div class="c-popup-edit-layout__wrapper l-wrapper">
      <div class="c-popup-edit-layout__heading-wrapper">
        <div class="c-popup-edit-layout__heading">
          <div class="c-heading c-heading--huge">Popup</div>
          <div class="c-popup-edit-layout__close" @click="close">
            <close-icon/>
          </div>
        </div>
      </div>
      <div class="c-popup-edit-layout__body">
        <edit-layout ref="layoutEditor" v-bind="$attrs" editable>
          <div class="l-page__footer">
            <button class="c-button c-button--secondary c-button--huge" @click="save">Save layout</button>
          </div>
        </edit-layout>
      </div>
    </div>
  </div>
</template>

<script>
  import EditLayout from '../components/EditLayout'
  import CloseIcon from './CloseIcon.vue'

  export default {
    name: 'PopupEditLayout',
    components: {
      CloseIcon,
      EditLayout},
    inheritAttrs: false,
    data () {
      return {
        isActive: false
      }
    },
    methods: {
      open () {
        this.isActive = true
      },
      close () {
        this.isActive = false
      },
      save () {
        const layoutEditor = this.$refs.layoutEditor
        const slot1 = layoutEditor.$refs.slot1
        const list1 = slot1.getDraggablePanelList()
        const slot2 = layoutEditor.$refs.slot2
        const list2 = slot2.getDraggablePanelList()
        let exportedLayout = {
          slot1: [],
          slot2: []
        }
        exportedLayout.slot2[0] = []
        exportedLayout.slot2[1] = []
        for (let i = 0; i < 4; i++) {
          let res = 0
          if (list1.hasOwnProperty(i)) {
            res = list1[i].id
          }
          exportedLayout.slot1[i] = res
        }
        for (let i = 0; i < 6; i++) {
          let res = 0
          if (list2.hasOwnProperty(i)) {
            res = list2[i].id
          }
          exportedLayout.slot2[i < 3 ? 0 : 1][i < 3 ? i : i - 3] = res
        }
        this.download('layout.json', JSON.stringify(exportedLayout))
      },
      download (filename, text) {
        let element = document.createElement('a')
        element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(text))
        element.setAttribute('download', filename)
        element.style.display = 'none'
        document.body.appendChild(element)
        element.click()
        document.body.removeChild(element)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .c-popup-edit-layout {
    $transition-time: 0.4s;
    @include position(fixed, 0);
    z-index: 9999;
    background-color: white;
    transition: transform $transition-time ease;

    &:not(.is-active) {
      visibility: hidden;
      opacity: 0;
      transform: translateY(10px);
    }
  }

  .c-popup-edit-layout__wrapper {
    height: 100%;
  }

  .c-popup-edit-layout__heading-wrapper {
    position: relative;
    height: 0;
  }

  .c-popup-edit-layout__heading {
    @include position(absolute, 0 0 null);
    width: 100%;
    max-width: 1200px;
    height: rem(80);
    line-height: rem(68);
  }

  .c-popup-edit-layout__heading .c-heading {
    color: black;
  }

  .c-popup-edit-layout .c-draggable-panel__heading {
    background-color: white !important;
  }

  .c-popup-edit-layout__body {
    height: 100%;
    padding-top: rem(80);
  }

  .c-popup-edit-layout__close {
    $width: 60px;
    @include position(absolute, 50% 0 null null);
    margin-top: (-$width / 2);
    width: $width;
    height: $width;
    line-height: $width;
    text-align: center;
    border-radius: 50%;
    background-color: #fafafc;
    cursor: pointer;

    &:hover {
      background-color: darken(#fafafc, 4%);
    }

    & svg {
      $width: 20px;
      display: block;
      @include position(absolute, 50% 50% null null);
      @include margin((-$width / 2) (-$width / 2) null null);
      width: $width;
      height:$width;
      fill: #333;
    }
  }
</style>
