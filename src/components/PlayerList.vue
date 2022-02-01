<template>
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
            pills
            :total-rows="rows"
            :per-page="perPage"
            aria-controls="my-table"
            class="player-list-pagination"
            v-model="currentPage"
        ></b-pagination>
    </div>
</template>

<script>
export default {
    props: {
        players: Array,
        showDetail: Function,
    },
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
            detail:'',
            perPage: 10,
            currentPage: '1',
        }
    },
    computed: {
        rows() {
            return this.players.length
        },
    },
    methods: {
        getPlayerDetail(player) {
            const detail = player
            this.showDetail(detail)
        },
    },
}
</script>

<style>
    .player-list-pagination{
        justify-content: center;
    }
</style>
