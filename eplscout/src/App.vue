<template>
  <div>{{ selectedTeam }}</div>
  <div>{{ selectedPlayer }}</div>

  <div
    @click="(selectedTeam = teams.id), teamFilter(teams.id)"
    v-for="(teams, i) in teams"
    :key="i"
  >
    {{ teams.name }}
  </div>

  <!-- <div>{{ teamFilteredPlayer[0] }}</div> -->
  <br />
  <div
    @click="(selectedPlayer = a.id), pickPlayer(a.id)"
    v-for="(a, i) in teamFilteredPlayer"
    :key="i"
  >
    {{ `${a.second_name}` }}
  </div>

  <div>{{ pickedPlayer }}</div>

  <!-- <div>{{ position[0] }}</div> -->
  <!-- <img :src="imgURL.replace('${code}', son.code)" />
  <h2>{{ son.first_name + " " + son.second_name }}</h2>
  <h4>value : {{ son.value_season }}</h4>
  <div v-for="(element, i) in son" :key="i">{{ i + ":" + element }}</div>
  <div>{{ imgURL.replace("${code}", son.code) }}</div> -->
</template>

<script>
// import jsonData from "./json/bootstrap-static.json";
import sonny from "./json/mock_son.json";
import axios from "axios";

// let dataURL = "https://fantasy.premierleague.com/api/bootstrap-static/";
let dataURL =
  "https://raw.githubusercontent.com/syrus-riius/mockserver/main/db.json";
let imgURL =
  "https://resources.premierleague.com/premierleague/photos/players/110x140/p${code}.png";

export default {
  name: "App",
  beforeMount() {
    axios.get(dataURL).then((res) => {
      this.data = res.data;
      this.teams = res.data.teams;
      this.players = res.data.elements;
      this.player_stats = res.data.elemnet_stats;
    });
  },
  // mounted() {
  //   console.log(rawData[0]);
  // },
  data() {
    return {
      data: [],
      teams: [],
      players: [],
      player_stats: [],
      selectedTeam: 0,
      teamFilteredPlayer: [],
      pickedPlayer: [],
      selectedPlayer: 0,
      // events: data.events,
      // game_settings: data.game_settings,
      // phases: data.phases,
      // teams: this.data.teams,
      // players: data.elements,
      // players_stats: data.element_stats,
      // position: data.element_types,
      // spurs: data.teams[16],
      // spursCode: 16,
      son: sonny,
      imgURL: imgURL,
      player17: [],
    };
  },

  methods: {
    teamFilter(teamCode) {
      this.teamFilteredPlayer = [];
      console.log("picked : " + teamCode);

      for (let i = 0; i < this.players.length; i++) {
        if (this.players[i].team === teamCode) {
          this.teamFilteredPlayer.push(this.players[i]);
        }
      }
      console.log(this.teamFilteredPlayer);
      return this.teamFilteredPlayer;
    },

    pickPlayer(playerCode) {
      this.pickedPlayer = [];

      console.log("picked : " + playerCode);
      let x = this.teamFilteredPlayer;
      console.log(x[0]);
      let findPlayer = x.filter((i) => i.id === playerCode);
      console.log(findPlayer);
      this.pickedPlayer = [...findPlayer];
    },
  },
  components: {},
};
</script>

<style>
#app {
  font-family: "Saira Condensed", sans-serif;
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 25px;
  margin-top: 60px;
}
</style>
