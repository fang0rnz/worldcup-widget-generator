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
    queryParams: Object
  },
  computed: {
    snippet() {
      const rawhtml = `<iframe frameborder="0" id="cup-matches" src="https://tribunaonline.com.br/api/copa/2018/jogos${
        this.getParams
      }" width="100%"></iframe>`;
      this.$emit('compute-html', rawhtml);
      return rawhtml;
    },
    getParams() {
      const { date, selectedTeam, isAbbreviated } = this.queryParams;

      return `?team=${selectedTeam}${date ? '&date=' + date : ''}${
        isAbbreviated ? '&abbr=true' : ''
      }`.toLowerCase();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.rendered-widget {
  min-height: 400px;
}
iframe#cup-matches {
  height: 116px !important;
}
</style>
