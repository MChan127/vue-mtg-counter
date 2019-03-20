<template>
  <transition name="menu">
    <div id="menu" v-if="show">
      <a v-on:click="routeTo('home')">Home</a>
      <a v-on:click="routeTo('about')">About</a>
    </div>
  </transition>
</template>

<script lang="ts">
  import {Component, Prop, Watch, Vue} from "vue-property-decorator";
  import router from "@/router";

  @Component
  export default class Menu extends Vue {
    @Prop(Boolean) private readonly show!: boolean;
    @Prop(Function) private readonly closeMenu!: Function;

    @Watch('show')
    onChildChanged(val: boolean, oldVal: boolean) {
      console.log('show menu changed', val, oldVal);
    }

    public routeTo(path: string): void {
      this.closeMenu();
      router.push({path});
    }
  }
</script>

<style scoped lang="scss">
  #menu {
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

      transition: all .3s;

      &:hover {
        background-color: #4FC93F;
      }
    }
  }

  .menu-enter-active, .menu-leave-active {
    transition: left .3s;
  }
  .menu-leave, .menu-enter-to {
    left: 0;
  }
  .menu-enter, .menu-leave-to /* .fade-leave-active below version 2.1.8 */ {
    left: -315px;
  }
</style>
