<template>

  <div>
    <div class="field">
      <div class="control">
        <label for="" class="label">Data do jogo</label>
        <input class="input" type="date" @input="pickDate">
      </div>
    </div>
    <div class="field">
      <label class="label">Nome da seleção abreviado?</label>
      <div class="control">
        <div class="onoffswitch">
          <input @input="toggleAbbreviation" type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch" checked>
          <label class="onoffswitch-label" for="myonoffswitch"></label>
        </div>
      </div>
    </div>
    <div class="field">
      <label for="" class="label">Selecione uma seleção</label>
      <div class="control">
        <div class="select">
          <select @input="pickTeam">
            <option :value="key" v-for="(team, key) in teams" :key="key">
              {{team}}
            </option>
          </select>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: 'SettingsPicker',
  props: {
    teams: Object
  },
  methods: {
    pickTeam(e) {
      this.$emit('select-input', e.target.value);
    },
    pickDate(e) {
      this.$emit('select-date', e.target.value);
    },
    toggleAbbreviation(e) {
      this.$emit('toggle-abbreviation', e.target.value);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.onoffswitch {
  position: relative;
  width: 55px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
}
.onoffswitch-checkbox {
  display: none;
}
.onoffswitch-label {
  display: block;
  overflow: hidden;
  cursor: pointer;
  height: 20px;
  padding: 0;
  line-height: 20px;
  border: 2px solid #ffffff;
  border-radius: 20px;
  background-color: #9e9e9e;
  transition: background-color 0.12s ease-in;
}
.onoffswitch-label:before {
  content: '';
  display: block;
  width: 20px;
  margin: 0px;
  background: #ffffff;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 33px;
  border: 2px solid #ffffff;
  border-radius: 20px;
  transition: all 0.12s ease-in 0s;
}
.onoffswitch-checkbox:checked + .onoffswitch-label {
  background-color: #42a5f5;
}
.onoffswitch-checkbox:checked + .onoffswitch-label,
.onoffswitch-checkbox:checked + .onoffswitch-label:before {
  border-color: #42a5f5;
}
.onoffswitch-checkbox:checked + .onoffswitch-label:before {
  right: 0px;
}
</style>
