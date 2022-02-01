<template>
    <div class="player-search">
        <b-form inline>
            <label class="mr-sm-2" for="inline-form-custom-select">Team</label>
            <b-form-select
            id="inline-form-custom-select"
            class="mb-2 mr-sm-2 mb-sm-0"
            v-model="team"
            :options="teams"
            :value="null"
            @change="searchTeam"
            >
            </b-form-select>

            <label class="mr-sm-2" for="inline-form-input-name">Keyword</label>
            <b-form-input
            id="inline-form-input-name"
            class="mb-2 mr-sm-2 mb-sm-0"
            placeholder="Name"
            v-model="keyword"
            @input="searchName"
            ></b-form-input>
        </b-form>
        
    </div>
</template>

<script>
import players from '../assets/players.json'

export default {
    props: {
        onSearchTeam: Function,
        onSearchName: Function,
    },
    data() {
        return {
            team: '',
            keyword: '',
        }
    },
    computed: {
        teams() {
            return Array.from(new Set(players.map(item => item.team_acronym)))
        }
    },
    methods: {
        getPlayers() { // 為了拿到隊名
            this.players = players
        },
        searchName(){
            const name = this.keyword
            this.onSearchName(name)
        },
        searchTeam(){
            const team = this.team
            this.onSearchTeam(team)
        }
    },
}

</script>

<style></style>