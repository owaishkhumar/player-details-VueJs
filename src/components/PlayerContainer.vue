<template>
    <div class="container text-center">
        <div v-if="filterPlayerData.length > 0">
            <div v-if="filterPlayerData.some(player => player.role === 2)" class="row batsman-row">
                <h1>Batsman</h1>
                <div class="card-container">
                    <PlayerCard v-for="(player, index) in filterPlayerData" :key="index" :player="player"
                        v-if="player.role === 2" />
                </div>
            </div>
            <div v-if="filterPlayerData.some(player => player.role === 4)" class="row bowler-row">
                <h1>Bowlers</h1>
                <div class="card-container" >
                    <PlayerCard v-for="(player, index) in filterPlayerData" :key="index" :player="player"
                        v-if="player.role === 4" />
                </div>
            </div>
            <br />
    
            <div v-if="filterPlayerData.some(player => player.role === 3)" class="row all-rounder-row">
                <h1>All rounders</h1>
                <div class="card-container">
                    <PlayerCard v-for="(player, index) in filterPlayerData" :key="index" :player="player"
                        v-if="player.role === 3" />
                </div>
            </div>
        </div>
        <div v-else>
            <h1>No Player Found</h1>
        </div>
    </div>
</template>

<script>
import PlayerCard from './PlayerCard.vue';

export default {
    name: 'PlayerContainer',
    components: {
        PlayerCard
    },
    props: {
        playersData: {
            type: Object,
            required: true
        },
        country: {
            type: String,
            default: 'ALL'
        },
        name: {
            type: String,
            default: ''
        }
    },
    computed: {
        filterPlayerData() {
            if (this.country === "ALL" && this.name === '') {
                return this.playersData.originalPlayers
            }
            else {
                return (this.playersData.originalPlayers).filter(p => (this.country === "ALL" || p.team_name === this.country) && (this.name ==='' || p.name.toLowerCase().includes(this.name.toLowerCase())))
            }
        }
    }
}
</script>

<style>
.card-container {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}
</style>