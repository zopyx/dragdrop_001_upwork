<template>
  <div class="c-viewport">
    <div class="c-viewport__header">
      <!-- // -->
    </div>
    <div class="l-wrapper c-viewport__body">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
  require('./assets/scss/_app.scss')

  export default {
    name: 'App'
  }
</script>

<style lang="scss" scoped>
  .c-viewport {
    display: flex;
    flex-wrap: nowrap;
    align-items: stretch;
    min-height: 100%;
    background-color: #c8cbd1;
  }

  .c-viewport__header {
    //
  }

  .c-viewport__body {
    background-color: #f2f3f7;
    box-shadow: 0 0 250px rgba(0, 0, 0, 0.03);
  }
</style>
