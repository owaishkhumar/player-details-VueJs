<template>
  <div id="app">
    <NavBar :playersData=playersData @country-selected="handleCountry" @name-selected="handleName" />
    <PlayerContainer :playersData="playersData" :country="country" :name="name" />

  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import PlayerContainer from './components/PlayerContainer.vue';

export default {
  name: 'app',
  components: {
    NavBar,
    PlayerContainer
  },
  data() {
    return {
      playersData: {},
      country: "ALL",
      name: ''
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      try {
        const response = await fetch('/players.json');
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        this.playersData = await response.json();
      } catch (error) {
        throw new Error('There was a problem with the fetch operation:', error);
      }
    },


    handleCountry(country) {
      this.country = country
    },
    handleName(name) {
      this.name = name
    }
  }

}
</script>

<style></style>
