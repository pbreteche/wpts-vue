<template>
    <form v-show="teams.length < 16" v-on:submit.prevent="add">
        <div>
            <label for="team.name">Nom</label>
            <input type="text" id="team.name" v-model="newTeamName">
        </div>
    </form>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class TeamCreation extends Vue {
    private newTeamName = '';

    private add() {
        this.$store.commit('addTeam', this.newTeamName);
        this.newTeamName = '';
    }
}
</script>

<style scoped>

</style>
