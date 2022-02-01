<template>
    <div class="player-detail">
        <div class="player-detail-conatin">

            <div class="player-detail-header">
                <div class="player-detail-header-user">
                    <img src='../assets/account.png'>
                    <div class="player-detail-header-userName">{{detail.name}}</div>
                </div>

                <div class="player-detail-header-close" @click="onClosePopup">
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
</template>

<script>
export default {
    props: {
        closePopup: Function,
        detail: Object,
        isShowDetail: Boolean,
    },
    methods: {
        onClosePopup() {
            const close = false
            this.closePopup(close)
        }
    },
}
</script>


<style>
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