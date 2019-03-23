<template>
  <div id="appWrapper">
    <div id="app">
      <b-button id="showNavBtn" v-on:click="toggleShowNav">{{showNav ? "Hide Nav" : "Show Nav"}}</b-button>
      <div id="logoWrapper">
        <img alt="LiVue Counter Logo" src="@/assets/livue_counter_logo.png" id="mainLogo">
      </div>
      <router-view/>
    </div>
    <Nav :show="showNav" :close-nav="closeNav"/>
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
    public showNav: boolean = false;

    public data() {
      return {
        showNav: false,
      };
    }

    public toggleShowNav() {
      this.showNav = !this.showNav;
    }

    public closeNav() {
      this.showNav = false;
    }
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
