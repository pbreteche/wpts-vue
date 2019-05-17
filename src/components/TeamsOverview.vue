<template>
  <div>
    <p>Équipe: {{ teams.length }} / 16 <button v-on:click="draw">Tirer</button></p>
    <ul>
      <li v-for="(team, index) in teams">
        <span v-on:click="showForm(index)" v-show="index!==editedTeam">{{ team.name }} (#{{team.id}})</span>
        <form v-on:submit.prevent="hideForm" v-show="index===editedTeam">
          <input v-model="teams[index].name">
        </form>
        <button v-on:click="remove(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class TeamsOverview extends Vue {

  private editedTeam = -1;

  private get teams() {
    return this.$store.state.teams;
  }

  private showForm(index: number) {
    this.editedTeam = index;
  }

  private hideForm() {
    this.editedTeam = -1;
  }

  private remove(index: number) {
    this.$store.commit('remove', index);
    this.editedTeam = -1;
  }

  private draw() {
    this.$store.commit('draw');
    this.$router.push('draw');
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #42b983;
}
</style>
