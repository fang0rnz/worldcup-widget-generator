<template>
  <div id="app">
    <div class="container">
      <h1 class="title">Gerador de widgets de jogos da Copa 🇧🇷 🇧🇷 🇧🇷 🏆 ⚽ </h1>
      <div class="columns">
        <div class="column is-one-third">
          <div class="card">
            <div class="card-content">
              <div class="media">
                <div class="media-content">
                  <SettingsPicker @toggle-abbreviation="isAbbreviated = !isAbbreviated" @select-date="date = $event" @select-input="selectedTeam = $event" :teams="teams"/>
                  <hr>
                  <label class="label">
                    Código gerado:
                  </label>
                  <div class="control">
                    <button class="button" data-clipboard-target="#snippet-source">
                      <img src="./assets/copy_icon.svg">&nbsp;&nbsp;Copiar código 
                    </button>
                    <textarea id="snippet-source" class="textarea" placeholder="Textarea" rows="6" readonly v-text="snippet"></textarea>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-two-thirds">
          <WidgetSource :snippet="snippet"/>
        </div>
      </div>
        <footer>
            <div class="content has-text-right has-text-centered-mobile">
              <a href="http://conceptho.com">
                <img class="img-logo" src="http://conceptho.com/img/logo-horizontal.png" alt="Logo da Conceptho"> 
              </a>
            </div>
        </footer> 
    </div>
  </div>
</template>

<script>
import SettingsPicker from './components/SettingsPicker.vue';
import WidgetSource from './components/WidgetSource.vue';

import ClipBoard from 'clipboard';

import teams from './assets/teams';

export default {
  name: 'app',
  components: {
    SettingsPicker,
    WidgetSource
  },
  data() {
    return {
      teams: teams.reduce((acc, { team, abbreviation }) => {
        acc[abbreviation] = team;
        return acc;
      }, {}),
      selectedTeam: '',
      date: null,
      isAbbreviated: true
    };
  },
  computed: {
    snippet() {
      const rawhtml = `<iframe frameborder="0" id="cup-matches" src="https://tribunaonline.com.br/api/copa/2018/jogos${
        this.getParams
      }" width="100%"></iframe>`;
      return rawhtml;
    },
    getParams() {
      const { date, selectedTeam, isAbbreviated } = this;
      return `?team=${selectedTeam}${date ? '&date=' + date : ''}${
        isAbbreviated ? '&abbr=true' : ''
      }`.toLowerCase();
    }
  },
  mounted() {
    new ClipBoard('.button');
  }
};
</script>

<style lang="scss">
@import '../node_modules/bulma/css/bulma.min.css';

.img-logo {
  width: 200px;

  filter: brightness(0) invert(1);
  @media (max-width: 692px) {
    width: 80%;
    margin-bottom: 10px;
  }
}

.title {
  color: mistyrose;
}

.widget {
  max-width: 400px;
}

.container {
  padding-top: 16px;
}

body {
  min-height: 100vh;
  background: #1e5799; /* Old browsers */
  background: -moz-linear-gradient(
    top,
    #1e5799 0%,
    #2989d8 50%,
    #7db9e8 100%
  ); /* FF3.6-15 */
  background: -webkit-linear-gradient(
    top,
    #1e5799 0%,
    #2989d8 50%,
    #7db9e8 100%
  ); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(
    to bottom,
    #1e5799 0%,
    #2989d8 50%,
    #7db9e8 100%
  ); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#1e5799', endColorstr='#7db9e8',GradientType=0 ); /* IE6-9 */
}

.button {
  margin-bottom: 6px;
}
</style>
