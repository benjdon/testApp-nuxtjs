<template>
  <v-app>
    <v-main class="main-bg-dark">
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </v-main>
    <v-footer app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator'

  @Component({})
  export default class DefaultLayout extends Vue {
  }
</script>