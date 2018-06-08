<template>
  <div id="app">
    <div class="container">
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
                    <textarea class="textarea" placeholder="Textarea" rows="6" readonly v-model="rawHtml"></textarea>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-two-thirds">
          <WidgetSource @compute-html="rawHtml = $event" :queryParams="{selectedTeam, date, isAbbreviated}"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SettingsPicker from './components/SettingsPicker.vue';
import WidgetSource from './components/WidgetSource.vue';

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
      selectedTeam: 'BRA',
      date: null,
      isAbbreviated: true,
      rawHtml: ''
    };
  }
};
</script>

<style>
@import '../node_modules/bulma/css/bulma.min.css';

.widget {
  max-width: 400px;
}

.container {
  padding-top: 10%;
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
</style>
