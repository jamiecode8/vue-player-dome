<template>
    <div class="player">
        <div class="player-header">
            <h1>Player List Demo</h1>
            <!-- <div class="player-header-user">這裡放頭像</div> -->
        </div>

        <player-search
            :search-team="onSearchTeam"
            :search-name="onSearchName"
            ></player-search>
        <!-- <div class="player-search">
            <div class="player-search-input"> 
                <b-form inline>
                    <label class="mr-sm-2" for="inline-form-custom-select">Team</label>
                    <b-form-select
                    id="inline-form-custom-select"
                    class="mb-2 mr-sm-2 mb-sm-0"
                    v-model="search.team"
                    :options="teams"
                    :value="null"
                    @change="onSearch"
                    >
                    </b-form-select>

                    <label class="mr-sm-2" for="inline-form-input-name">Keyword</label>
                    <b-form-input
                    id="inline-form-input-name"
                    class="mb-2 mr-sm-2 mb-sm-0"
                    placeholder="Name"
                    v-model="search.keyword"
                    @input="onSearch"
                    ></b-form-input>
                </b-form>
            </div>
        </div> -->

        <div class="player-list">
            <b-table 
                id="my-table"
                striped hover 
                :items="players" 
                :fields="fields"
                :per-page="perPage"
                :current-page="currentPage"
                @row-clicked="getPlayerDetail"
            ></b-table>
            <b-pagination
                v-model="currentPage"
                :total-rows="rows"
                :per-page="perPage"
                aria-controls="my-table"
                class="player-list-pagination"
            ></b-pagination>
        </div>

        <div v-if="detail !=''">
            <div class="player-detail" v-show="showDetail">
                <div class="player-detail-conatin">

                    <div class="player-detail-header">
                        <div class="player-detail-header-user">
                            <img src='../assets/account.png'>
                            <div class="player-detail-header-userName">{{detail.name}}</div>
                        </div>

                        <div class="player-detail-header-close" @click="closePopup">
                            <img src="../assets/close.png">
                        </div>
                    </div>

                    <div class="player-detail-conatin-body">
                        <ul>
                            <li>Team : {{detail.team_acronym}}</li>
                            <li>TeamName: {{detail.team_name}}</li>
                            <li>Games: {{detail.games_played}}</li>
                            <li>MPG: {{detail.minutes_per_game}}</li>
                            <li>FGA: {{detail.field_goals_attempted_per_game}}</li>
                            <li>FGM: {{detail.field_goals_made_per_game}}</li>
                            <li>FG% : {{detail.field_goal_percentage}}</li>
                            <li>FT% : {{detail.free_throw_percentage}}</li>
                            <li>3PA : {{detail.three_point_attempted_per_game}}</li>
                            <li>3PM  : {{detail.three_point_made_per_game}}</li>
                            <li>3PT% : {{detail.three_point_percentage}}</li>
                            <li>Points  : {{detail.points_per_game}}</li>
                            <li>ORebounds  : {{detail.offensive_rebounds_per_game}}</li>
                            <li>DRebounds : {{detail.defensive_rebounds_per_game}}</li>
                            <li>Rebounds : {{detail.rebounds_per_game}}</li>
                            <li>Assists : {{detail.assists_per_game}}</li>
                            <li>Steals : {{detail.steals_per_game}}</li>
                            <li>Blocks : {{detail.blocks_per_game}}</li>
                            <li>Turnovers : {{detail.turnovers_per_game}}</li>
                            <li>Efficiency : {{detail.player_efficiency_rating}}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        
    </div>
</template>


<script>
import players from '../assets/players.json'
import PlayerSearch from './PlayerSearch.vue'

export default {
    components: { PlayerSearch },
    data() {
        return {
            fields: [
                {
                    key: 'team_acronym',
                    label: 'Team',
                    sortable: true
                },
                {
                    key: 'name', 
                    label: 'Name',
                    sortable: true
                },
                {
                    key: 'points_per_game', 
                    label: 'points',
                    sortable: true
                },
                {
                    key: 'rebounds_per_game', 
                    label: 'rebounds',
                    sortable: true
                },
                {
                    key: 'assists_per_game', 
                    label: 'assists',
                    sortable: true
                },
                {
                    key: 'steals_per_game', 
                    label: 'steals',
                    sortable: true
                },
                {
                    key: 'blocks_per_game', 
                    label: 'blocks',
                    sortable: true
                },
                ],
            players: [],
            detail: [],
            perPage: 10,
            currentPage: 1,
            showDetail: false,
        }
    },
    computed: {
        rows() {
            return this.players.length
        },
        teams() {
            return Array.from(new Set(players.map(item => item.team_acronym)))
        }
    },
    methods: {
        getPlayers() {
            this.players = players
        },
        onSearchTeam(team) { // value是組件傳來的值 搜尋隊名
            const searchTeam = team
                this.players = players.filter(item => 
                    item.team_acronym === searchTeam)
        },
        onSearchName(name) { // value是組件傳來的值 搜尋隊名
            const searchNeam = name
                this.players = players.filter(item => 
                    item.name === searchNeam)
        },
        onSearch() {
            const searchTeam = this.search.team
            const searchNeam = this.search.keyword

            if(searchTeam !=''){
                this.players = players.filter(item => 
                    (item.team_acronym === searchTeam) &&
                    (item.name === '' || item.name.indexOf(searchNeam) != -1 ))
            }else{
                this.players = players.filter(item =>
                    (item.name === '' || item.name.indexOf(searchNeam) != -1 ))
            }
        },
        getPlayerDetail(player) {
            this.detail = player
            this.showDetail = true
        },
        closePopup() {
            this.showDetail = false
        }
    },
    mounted() {
        this.getPlayers()
    },

}
</script>

<style>
    .player-header{
        padding: 5px 15px ;
    }
    .player-search{
        background-color : #f2f2f2;
        display : flex;
        justify-content: center;
        padding: 60px 150px;
    }
    .player-list-pagination{
        justify-content: center;
    }
    .player-detail{
        background-color: rgba(14,14,14,0.5);
        width: 100%;
        height: 100%;
        position: fixed;
        top: 0;
        left: 0;
        z-index: 900;
    }
    .player-detail-conatin{
        position: fixed;
        width: 70%;
        height: fit-content;
        top: 150px;
        left: 15%;
        padding: 20px;
        background-color:white;
    }
    .player-detail-header{
        display: flex;
        padding-bottom: 5px;
        border-bottom: solid 1px #f2f2f2;
    }
    .player-detail-header-user{
        display: flex;
    }
    .player-detail-header-userName{
        line-height: 50px;
    }
    .player-detail-header-close{
        position: absolute;
        top: 20px;
        right: 20px;
    }
    .player-detail-conatin-body{
        padding-top: 10px;
    }

</style>