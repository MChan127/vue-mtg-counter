<template>
  <div class="player">
    <div class="playerData">
      <h1 class="playerNumber">Player {{this.playerNum}}</h1>
      <p class="playerLifeCount">{{this.lifeCount}}</p>
    </div>
    <ul class="playerMenu">
      <li v-on:click="callUpdateLife(-5)">-5</li>
      <li v-on:click="callUpdateLife(-1)">-1</li>
      <li v-on:click="callUpdateLife(1)">+1</li>
      <li v-on:click="callUpdateLife(5)">+5</li>
    </ul>
  </div>
</template>

<script lang="ts">
  import {Component, Prop, Vue} from "vue-property-decorator";

  @Component
  export default class Player extends Vue {
    @Prop(String) private readonly playerNum!: string;
    @Prop(Number) private lifeCount!: number;
    @Prop(Function) private readonly updateLife!: (playerNum: string, delta: number) => void;

    public callUpdateLife(delta: number) {
      this.updateLife(this.playerNum, delta);
    }
  }
</script>

<style lang="scss">
  $roundedCorner: 10px;
  .player {
    border-radius: $roundedCorner;
    box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.35);
    margin: 20px 0 0 0;

    .playerData {
      padding: 10px;

      .playerNumber {
        text-align: center;
        font-size: 30px;
        margin: 0;
      }
      .playerLifeCount {
        text-align: center;
        font-size: 60px;
        margin: 0;
      }
    }

    $btnHeight: 35px;
    .playerMenu {
      width: 100%;
      margin: 0;
      padding: 0;
      list-style-type: none;
      border-top: 1px solid #ccc;

      li {
        display: inline-block;
        width: 25%;
        height: $btnHeight;
        line-height: $btnHeight;
        text-align: center;
        cursor: pointer;

        &:first-child {
          border-bottom-left-radius: $roundedCorner;
        }
        &:last-child {
          border-bottom-right-radius: $roundedCorner;
        }

        &:not(:last-child) {
          border-right: 1px solid #ccc;
        }

        &:hover {
          transition: all 0.2s;
          background-color: #eee;
        }
      }
    }
  }
</style>
