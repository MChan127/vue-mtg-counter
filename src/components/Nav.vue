<template>
  <transition name="nav">
    <div id="nav" v-if="show">
      <a v-on:click="routeTo('home')">Home</a>
      <a v-on:click="routeTo('about')">About</a>
      <a id="closeMenuBtn" v-on:click="closeNav()">Close Menu</a>
    </div>
  </transition>
</template>

<script lang="ts">
  import {Component, Prop, Watch, Vue} from "vue-property-decorator";
  import router from "@/router";

  @Component
  export default class Nav extends Vue {
    @Prop(Boolean) private readonly show!: boolean;
    @Prop(Function) private readonly closeNav!: () => void;

    /*@Watch('show')
    onChildChanged(val: boolean, oldVal: boolean) {
      console.log('show nav changed', val, oldVal);
    }*/

    public routeTo(path: string): void {
      this.closeNav();
      router.push({path});
    }
  }
</script>

<style scoped lang="scss">
  #nav {
    position: absolute;
    top: 0;
    height: 100vh;
    width: 300px;
    background-color: #4FC93F;
    border-right: 15px solid #000;

    a {
      cursor: pointer;
      color: #fff;
      font-size: 24px;
      font-weight: 600;
      padding: 10px 0;
      margin-bottom: 10px;
      display: block;
      text-decoration: none;
      background-color: #47a447;
      text-align: center;

      transition: all .3s;

      &:hover {
        background-color: #4FC93F;
      }
    }

    /*#closeMenuBtn {
      display: none;

      @media only screen and (max-width: 480px) {
        display: block;
      }
    }*/
  }

  .nav-enter-active, .nav-leave-active {
    transition: left .3s;
  }
  .nav-leave, .nav-enter-to {
    left: 0;
  }
  .nav-enter, .nav-leave-to /* .fade-leave-active below version 2.1.8 */ {
    left: -315px;
  }
</style>
