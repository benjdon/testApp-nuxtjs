<template>
  <v-alert
    type="error"
    class="py-2 mt-5"
    :value="showErrorMsg"
    v-html="errorMsg">
  </v-alert>
</template>

<script lang="ts">
  import { Component, Vue, Prop } from 'vue-property-decorator'

  @Component({})
  export default class ErrorAlert extends Vue {
    @Prop({ default: false }) readonly showErrorMsg!: boolean;
    @Prop({ default: false }) readonly errorMsg!: boolean;
  }
</script>
