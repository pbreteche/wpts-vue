<template>
    <div>
        <div class="pools">
            <table v-for="(pool, index) in pools">
                <tr>
                    <th>Poule {{ index }}</th>
                    <th v-for="(team) in pool">{{ team.name }}</th>
                </tr>
                <tr v-for="(teamA, i) in pool">
                    <th>{{ teamA.name }}</th>
                    <td v-for="(teamB, j) in pool" v-bind:class="{blur: i === j}" contenteditable="true"
                    @blur="addScore($event, teamA, teamB)"></td>
                </tr>
            </table>
        </div>
        <form>
            <div>Vainqueur
            <label>
                <input type="radio">
                {{ teamA.name }}
            </label>
            <label>
                <input type="radio">
                {{ teamB.name }}
            </label>
            </div>
        </form>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import {Team} from "@/model/Team";

@Component
export default class Pool extends Vue {
    private teamA = new Team();
    private teamB = new Team();

    private get pools() {
        return this.$store.state.tournament.pools;
    }

    addScore(evt: Event, teamA: Team, teamB: Team) {
        console.log(teamA, teamB, evt.target.innerText)
        this.teamA = teamA;
        this.teamB = teamB;
    }
}
</script>

<style scoped>
    .pools {
        display: flex;
        flex-flow: row wrap;
        justify-content: space-evenly;
    }

    table, th, td {
        border: 1px solid;
        border-collapse: collapse;
    }

    td, th {
        padding: .5em;
    }

    th {
        background-color: #2c3e50;
        color: aliceblue;
    }

    .blur {
        background-color: #2c3e50;
    }
</style>
