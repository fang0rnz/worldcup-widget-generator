<template>
  <div class="hello">
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
.rendered-widget {
  height: 582.55px;
  background-color: white;
}
iframe#cup-matches {
  height: 582.55px !important;
}
</style>
