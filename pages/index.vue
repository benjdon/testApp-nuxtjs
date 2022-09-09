<template>
  <div id="login-container">
    <v-card outlined height="500" width="850" class="d-flex align-center mx-auto rounded-0">
      <div style="width: 100%">
        <v-card flat class="ma-auto" width="500">
        <v-card-title class="d-block text-center">
          <h1 class="grey--text text--darken-3 mt-5">Welcome to TestApp</h1>
        </v-card-title>
        <v-card-text class="text-center mt-10">
          <v-btn
            small 
            elevation="1"
            class="mr-5 brand-color"
            @click="$router.push('/people')">
            View List of People
          </v-btn>
        </v-card-text>
        </v-card>
      </div>
    </v-card>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator'

  @Component({})
  export default class IndexPage extends Vue {
  }
</script>

