<template>
  <div class="home">
    <b-container>
      <b-row>
        <b-col col-sm="4">
          <b-button class="menuBtn" variant="outline-primary">Reset</b-button>
        </b-col>
        <b-col col-sm="4">
          <b-button class="menuBtn" variant="outline-primary">Reset</b-button>
        </b-col>
        <b-col col-sm="4">
          <b-button class="menuBtn" variant="outline-primary">Reset</b-button>
        </b-col>
        <b-col col-sm="4">
          <b-button class="menuBtn" variant="outline-primary">Reset</b-button>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class Home extends Vue {

}
</script>

<style lang="scss">
  .menuBtn {
    width: 100%;
  }
</style>

