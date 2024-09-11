<template>
    <div class="card">
        <ul class="list-group list-group-flush">
            <li class="list-group-item"><b>Name </b>{{ player.name }}</li>
            <li class="list-group-item"><b>Matches </b> {{ player.matches }}</li>
            <li class="list-group-item"><b>Runs </b> {{ player.runs }}</li>
            <li class="list-group-item"><b>50s </b> {{ player['50s'] }}</li>
            <li class="list-group-item"><b>100s </b> {{ player['100s'] }}</li>
            <li class="list-group-item" v-if="player.role === 2 || player.role === 3"><b>Highest Score </b> {{ player.highest_score }}</li>
            <li class="list-group-item" v-if="player.role === 4 || player.role === 3"><b>Best Bowling </b> {{ player.best_bowling_figures }}</li>
            <li class="list-group-item"><b>Team Name </b> {{ player.team_name }}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'PlayerCard',
        props: {
        player: {
            type: Object,
            required: true
        }
    },
    }
</script>

<style scoped>
.card{
    width: 16rem;
    margin: 10px;
}
</style>