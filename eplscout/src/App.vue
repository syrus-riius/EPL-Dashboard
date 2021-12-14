<template>
  <button @click="spursFilter()">SPURS</button>

  <div v-if="player17 === true">
    <div v-for="(player, i) in player17" :key="i">{{ player }}</div>
  </div>
  <div></div>
  <img :src="imgURL.replace('${code}', son.code)" />
  <h2>{{ son.first_name + " " + son.second_name }}</h2>
  <h4>value : {{ son.value_season }}</h4>
  <div v-for="(element, i) in son" :key="i">{{ i + ":" + element }}</div>
  <!-- <div>{{ imgURL.replace("${code}", son.code) }}</div> -->
</template>

<script>
import Bootstrap_stats from "./json/bootstrap-static.json";
import sonny from "./json/mock_son.json";

let imgURL =
  "https://resources.premierleague.com/premierleague/photos/players/110x140/p${code}.png";

export default {
  name: "App",
  data() {
    return {
      data1: Bootstrap_stats,
      teams: Bootstrap_stats.teams,
      spurs: Bootstrap_stats.teams[16],
      spursCode: 16,
      players: Bootstrap_stats.elements,
      son: sonny,
      imgURL: imgURL,
      player17: "",
    };
  },
  methods: {
    spursFilter() {
      console.log(this.players.length);

      let spursPlayer = [];
      for (let i = 0; i < this.players.length; i++) {
        let player = this.players[i];

        if (player.team === 17) {
          console.log(player.second_name);
          spursPlayer.push(player.first_name + " " + player.second_name);
        }
      }
      this.player17 = spursPlayer.join("\n");
    },
  },
  components: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
