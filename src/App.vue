<template>
  <div id="app">
    <div id="showMenuBtn" v-on:click="toggleShowMenu">{{showMenu ? "Hide Menu" : "Show Menu"}}</div> <img alt="LiVue Counter Logo" src="@/assets/livue_counter_logo.png" id="mainLogo">
    <Menu :show="showMenu" :close-menu="closeMenu" />
    <router-view/>
  </div>
</template>

<script lang="ts">
  import {Component, Vue} from "vue-property-decorator";
  import Menu from "@/components/Menu.vue";

  @Component({
    components: {
      Menu,
    },
  })
  export default class App extends Vue {
    public showMenu: boolean = false;

    public data() {
      return {
        showMenu: false,
      };
    }

    public toggleShowMenu() {
      this.showMenu = !this.showMenu;
    }

    public closeMenu() {
      this.showMenu = false;
    }
  }
</script>

<style lang="scss">
body {
  margin: 15px 0 0 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
#showMenuBtn {
  cursor: pointer;
}
#mainLogo {
  height: 150px;
  width: auto;
}
</style>
