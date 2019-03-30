<template>
  <div id="appWrapper">
    <div id="app">
      <b-button id="showNavBtn" v-on:click="toggleShowNav">{{showNav ? "Hide Nav" : "Show Nav"}}</b-button>
      <div id="logoWrapper">
        <img alt="LiVue Counter Logo" src="@/assets/livue_counter_logo.png" id="mainLogo">
      </div>
      <p style="text-align: center;">A life counter webapp for <i>Magic the Gathering</i> made in Vue.js</p>
      <router-view :game-data="this.gameData" :game-methods="this.gameMethods" :dice-roll-result="diceRollResult"/>
    </div>
    <Nav :show="showNav" :close-nav="closeNav"/>

    <b-modal ref="newGameModal" title="Start a New Game" @ok="confirmNewGame">
      <div class="d-block">
        <b-form-group label="# of Players">
          <b-form-radio-group
            id="newGameNumberOfPlayers"
            buttons
            button-variant="outline-primary"
            v-model="newGameData.numberOfPlayers"
            :options="newGameOptions.numberOfPlayers"
            name="newGameNumberOfPlayers"
            :native-value="2"
          />
        </b-form-group>

        <b-form-group label="Starting Life Count">
          <b-form-radio-group
            id="newGameStartingLifeCount"
            buttons
            button-variant="outline-primary"
            v-model="newGameData.startingLifeCount"
            :options="newGameOptions.startingLifeCount"
            name="newGameStartingLifeCount"
            :native-value="20"
          />
        </b-form-group>
      </div>
    </b-modal>
  </div>
</template>

<script lang="ts">
  import {Component, Vue} from "vue-property-decorator";
  import Nav from "@/components/Nav.vue";

  @Component({
    components: {
      Nav,
    },
  })
  export default class App extends Vue {
    // @ts-ignore
    public $data: IAppData;
    public showNav: boolean = false;

    public data() {
      return {
        showNav: false,
        diceRollResult: null,
        gameData: {
          players: {
            "1": 20,
            "2": 20,
          },
        },
        gameMethods: {
          updateLife: this.updateLife,
          newGame: this.newGame,
          rollDice: this.rollDice,
        },
        newGameData: {
          numberOfPlayers: 2,
          startingLifeCount: 20,
        },
        newGameOptions: {
          numberOfPlayers: [
            {text: "2", value: 2},
            {text: "3", value: 3},
            {text: "4", value: 4},
            {text: "5", value: 5},
            {text: "6", value: 6},
            {text: "7", value: 7},
            {text: "8", value: 8},
          ],
          startingLifeCount: [
            {text: "20", value: 20},
            {text: "30", value: 30},
            {text: "40", value: 40},
          ],
        },
      };
    }

    public toggleShowNav() {
      this.showNav = !this.showNav;
    }

    public closeNav() {
      this.showNav = false;
    }

    public updateLife(playerNum: string, delta: number) {
      // add to history log
      // TODO

      // update player life count
      this.$data.gameData.players[playerNum] += delta;
    }

    public newGame() {
      (this.$refs.newGameModal as any).show();
    }

    public confirmNewGame() {
      const numberOfPlayers: number = parseInt(this.$data.newGameData.numberOfPlayers, 10);
      const startingLifeCount: number = parseInt(this.$data.newGameData.startingLifeCount, 10);

      // perform form validation
      if (!(numberOfPlayers && startingLifeCount)) {
        alert("You must select a starting number of players and life count.");
        return;
      }

      // clear history log
      // TODO

      const newGameData: IGameData = {
        players: {},
      };
      let i: number;
      for (i = 0; i < numberOfPlayers; i++) {
        newGameData.players[(i + 1) + ""] = startingLifeCount;
      }
      this.$data.gameData = newGameData;

      (this.$refs.newGameModal as any).hide();
    }

    public rollDice() {
      const random: number = Math.floor(Math.random() * parseInt(this.$data.newGameData.numberOfPlayers, 10)) + 1;
      this.$data.diceRollResult = random.toString();
    }
  }

  export interface IAppData {
    showNav: boolean;
    diceRollResult: string;
    gameData: IGameData;
    gameMethods: IGameMethods;
    newGameData: INewGameData;
    newGameOptions: INewGameOptions;
  }
  export interface IGameData {
    players: IPlayerData;
  }
  export interface IPlayerData {
    [playerNum: string]: number;
  }
  export interface IGameMethods {
    updateLife: (playerNum: string, delta: number) => void;
    newGame: () => void;
    rollDice: () => void;
  }
  export interface INewGameData {
    numberOfPlayers: string;
    startingLifeCount: string;
  }
  export interface INewGameOptions {
    numberOfPlayers: any;
    startingLifeCount: any;
  }
</script>

<style lang="scss">
  body {
    margin: 15px 0 0 0;
  }

  #appWrapper {

  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    width: 50vw;
    margin: 0 auto;
  }

  /*#nav {
    padding: 30px;
    a {
      font-weight: bold;
      color: #2c3e50;
      &.router-link-exact-active {
        color: #42b983;
      }
    }
  }*/

  #showNavBtn {
    margin: 15px;
    cursor: pointer;
  }

  #logoWrapper {
    width: 100%;
    margin: 15px 0;
    text-align: center;

    #mainLogo {
      height: 150px;
      width: auto;
    }
  }
</style>
