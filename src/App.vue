<template>
  <div id="app">

    <div class="player-header">
        <h1>Player List Demo</h1>
        <!-- <div class="player-header-user">這裡放頭像</div> -->
    </div>

    <player-search
        :onSearchTeam="onSearchTeam"
        :onSearchName="onSearchName"
    ></player-search>

    <player-list
        :players = "players"
        :showDetail="showDetail"
    ></player-list>

    <player-detail
        v-if="isShowDetail"
        :detail = "detail"
        :isShowDetail ="isShowDetail"
        :closePopup ="closePopup"
    ></player-detail>

  </div>
</template>

<script>
import players from './assets/players.json'

import PlayerSearch from './components/PlayerSearch.vue'
import PlayerList from './components/PlayerList.vue'
import PlayerDetail from './components/PlayerDetail.vue'

export default {
  name: 'App',
  components: {
    PlayerSearch, PlayerList, PlayerDetail
  },
      data() {
        return {
            players: [], 
            detail: [],
            isShowDetail: false,
            searchTeam: '',
            searchNeam: '',
        }
    },
    methods: {
        getPlayers() {
            this.players = players
        },
        onSearchTeam(team) {
            this.searchTeam = team
            this.players = players.filter(item => 
                item.team_acronym === this.searchTeam)
        },
        onSearchName(name) {
            this.searchNeam = name
            if(this.searchTeam !=''){
                this.players = players.filter(item => 
                (item.team_acronym === this.searchTeam) &&
                (item.name === '' || item.name.indexOf(this.searchNeam) != -1 ))
            }
        },
        showDetail(player) {
            this.detail = player
            this.isShowDetail = true
        },
        closePopup(state) {
            this.isShowDetail = state
        }
    },
    mounted() {
        this.getPlayers()
    },

}
</script>

<style lang="scss">
@import "~@/assets/scss/vendors/bootstrap-vue/index";

</style>
