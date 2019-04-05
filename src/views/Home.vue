<template>
  <div class="home">
    <b-container>
      <b-row>
        <b-col md="4" sm="12" xs="12">
          <b-button class="menuBtn" variant="outline-primary" v-on:click="gameMethods.newGame">
            <font-awesome-icon :icon="['fa', 'power-off']"/>
            New Game
          </b-button>
        </b-col>
        <b-col md="4" sm="12" xs="12">
          <b-button class="menuBtn" variant="outline-primary" v-on:click="gameMethods.rollDice">
            <font-awesome-icon :icon="['fa', 'dice']"/>
            Roll
          </b-button>
        </b-col>
        <b-col md="4" sm="12" xs="12">
          <b-button class="menuBtn" variant="outline-primary">
            <font-awesome-icon icon="scroll"/>
            History
          </b-button>
        </b-col>
        <!--<b-col col-sm="4">
          <b-button class="menuBtn" variant="outline-primary">
            <font-awesome-icon icon="users"/>
            Players
          </b-button>
        </b-col>-->
      </b-row>

      <b-row class="diceRollResult" v-if="diceRollResult">
        <b-col>
          <p>{{"Player " + diceRollResult + " goes first!"}}</p>
        </b-col>
      </b-row>

      <b-row>
        <b-col sm="6" xs="12" v-for="(life, index) in this.gameData.players">
          <Player :player-num="index" :life-count="life" :update-life="gameMethods.updateLife" />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";
  import Player from "@/components/Player.vue";
  import {IGameData, IGameMethods} from "@/App.vue";

  @Component({
    components: {
      Player,
    },
  })
  export default class Home extends Vue {
    @Prop(Object) private gameData!: IGameData;
    @Prop(Object) private readonly gameMethods!: IGameMethods;
    @Prop(String) private readonly diceRollResult!: string;
  }
</script>

<style lang="scss">
  .menuBtn {
    width: 100%;

    @media only screen and (max-width: 767px) {
      margin-bottom: 15px;
    }
  }
  .diceRollResult {
    margin: 15px 0 0 0;
    p {
      margin: 0;
      text-align: center;
    }
  }
</style>

