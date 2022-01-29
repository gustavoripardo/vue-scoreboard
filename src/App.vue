<template>
  <div class="container">
    <transition-group class="container" :appear="true">
      <div class="header" :key="'header'">
        <h1>SCOREBOARD</h1>
      </div>
      <div class="body" :key="'body'">
        <Counter name="PSG" locationTeam="local" />
        <Counter name="Real Madrid" locationTeam="guest" />
      </div>
      <OtherGames
        :listGames="games"
        :key="'games'"
        @onGameClicked="onGameClicked($event)"
      />
    </transition-group>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

import Counter from "@/components/Counter.vue";
import OtherGames from "@/components/OtherGames.vue";

import Game from "@/interfaces/Game";

export default defineComponent({
  components: {
    Counter,
    OtherGames,
  },
  data() {
    return {
      games: [
        {
          id: 1,
          teamLocalName: "Team A",
          teamGuestName: "Team B",
          teamLocalGols: 0,
          teamGuestGols: 0,
        },
        {
          id: 2,
          teamLocalName: "Team C",
          teamGuestName: "Team D",
          teamLocalGols: 0,
          teamGuestGols: 0,
        },
        {
          id: 3,
          teamLocalName: "Team E",
          teamGuestName: "Team F",
          teamLocalGols: 0,
          teamGuestGols: 0,
        },
      ] as Game[],
    };
  },
  methods: {
    onGameClicked(event: number): void {
      alert(event);
      return;
    },
    teamsBackground() {
      let teams = this.games;
      teams.shift();
      console.log("teams: ", teams);
      return teams;
    },
    onGolLocalChange(value: number): void {
      this.games[0].teamLocalGols = value;
      return;
    },
    onGolGuestChange(value: number): void {
      this.games[0].teamGuestGols = value;
      return;
    },
  },
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&display=swap");

* {
  font-family: "Poppins", Arial, Helvetica, sans-serif;
}

body,
html {
  background-color: #577590;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

div {
  transition: all 0.5s linear;
}
button {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.btn-primary {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.btn-success {
  color: #fff;
  background-color: #28a745;
  border-color: #28a745;
}

.btn-light {
  color: #212529;
  background-color: #f8f9fa;
  border-color: #f8f9fa;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  align-content: center;
  background-color: #fff;
  border-radius: 15px;
  padding: 15px;
  width: 70vw;
  transition: all 0.5s linear;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px,
    rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px,
    rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
}

.body {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 50vw;
  margin-top: 30px;
  margin-bottom: 30px;
  background-color: transparent;
  border-radius: 30px;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s;
}

.localTeam {
  background-color: #90be6d;
}

.guestTeam {
  background-color: #f9844a;
}
</style>
