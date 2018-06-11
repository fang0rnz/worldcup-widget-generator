<template>
  <div class="widget-container">
    <div class="field">
      <div class="rendered-widget" v-html="snippet"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WidgetSource',
  props: {
    snippet: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.widget-container {
  height: 592px;
}
.rendered-widget {
  height: 592px;
  background-color: white;
}
iframe#cup-matches {
  height: 592px !important;
}
</style>
