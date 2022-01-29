<template>
  <button class="btn-light" type="button" @click="showMore = !showMore">
    Other games
  </button>

  <div class="list">
    <transition-group
      enter-active-class="animate__animated animate__backInUp"
      leave-active-class="animate__animated animate__backOutDown"
      :appear="showMore"
    >
      <div v-if="showMore">
        <div class="list-item" v-for="game in games" :key="game.id">
          <div class="item localTeam">
            {{ game.teamLocalName }}
            <div class="gols animate__animated animate__bounce">
              {{ game.teamLocalGols }}
            </div>
          </div>
          <div class="divider">VS</div>
          <div class="item guestTeam">
            <div class="gols animate__animated animate__bounce">
              {{ game.teamGuestGols }}
            </div>
            {{ game.teamGuestName }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
  {{ randomGols() }}
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";

import Game from "@/interfaces/Game";

export default defineComponent({
  props: {
    listGames: {
      type: [] as PropType<Game[]>,
      require: true,
    },
  },
  data() {
    return {
      games: this.$props.listGames as Game[],
      showMore: true,
    };
  },
  methods: {
    showGames(): boolean {
      return this?.games?.length > 0;
    },
    randomGols() {
      const timer = setInterval(() => {
        const percent = Math.random();
        if (percent >= 0.6) {
          const random = Math.floor(Math.random() * this.games.length);

          let teamGol = ["local", "guest"];
          let teamPick = Math.floor(Math.random() * teamGol.length);

          if (teamPick == 0) {
            this.games[random].teamLocalGols++;
          } else {
            this.games[random].teamGuestGols++;
          }
        }
      }, 1000);
    },
  },
});
</script>

<style scoped>
.other-games-header {
  width: 30vw;
  display: flex;
  justify-content: center;
}

.list {
  display: flex;
  flex-direction: column;
}

.list-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  margin-top: 10px;
  margin-bottom: 10px;
}

.item {
  padding: 15px;
  margin-left: 5px;
  margin-right: 5px;
  display: flex;
  flex-direction: row;
  border-radius: 15px;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.divider {
  display: flex;
  justify-content: center;
  align-items: center;
}

.gols {
  background-color: #fff;
  margin-left: 5px;
  margin-right: 5px;
  border-radius: 15px;
  padding: 5px;
  color: #000;
}
</style>
