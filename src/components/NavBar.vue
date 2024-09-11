<template>
    <nav class="navbar navbar-expand-lg bg-light">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Sportz Interactive</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <select name="team" id="team" v-model="country" @change="updateSelectedCountry">
                        <option value="ALL">ALL</option>
                        <option v-for="(team, index) in uniqueTeams" :key="index">{{ team }}</option>
                    </select>
                </ul>
                <form class="d-flex" role="search" @submit.prevent="updateName">
                    <input class="form-control me-2" v-model="name" type="search" placeholder="Search" id="searchInput" />
                    <button class="btn btn-outline-success" type="submit" id="searchButton"
                    onclick="searchPlayers()">Search</button>
                </form>
            </div>
        </div>
    </nav>
</template>

<script>
export default {
    name: 'Navbar',
    data() {
        return {
            country: "ALL",
            name: ''
        }
    },
    props: {
        playersData: {
            type: Object,
            required: true
        }
    },
    computed: {
        uniqueTeams() {
            if (this.playersData && Array.isArray(this.playersData.originalPlayers)) {
                const teams = this.playersData.originalPlayers.map(player => player.team_name);
                return this.removeDuplicates(teams);
            }
            return [];
        }
    },
    methods: {
        removeDuplicates(array) {
            const uniqueArray = [];
            for (const item of array) {
                if (!uniqueArray.includes(item)) {
                    uniqueArray.push(item);
                }
            }
            return uniqueArray;
        },
        updateSelectedCountry() {
            this.$emit('country-selected', this.country);
        },
        updateName() {
            this.$emit('name-selected', this.name);
        },
    }
}
</script>