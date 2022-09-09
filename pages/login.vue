<template>
  <div id="login-container">
    <v-card height="500" width="850" class="d-flex align-center mx-auto rounded-0">
      <div class="w-100">
        <v-card flat class="px-5 ma-auto" width="400">
          <v-card-title class="d-block text-center">
              <h2 class="grey--text text--darken-3 mt-5">Sign in to TestApp</h2>
          </v-card-title>
          <v-card-text class="text-center mt-3">
            <v-form ref="form" lazy-validation @submit="login" onSubmit="return false;">
              <v-text-field
                v-model="userInfo.username"
                outlined
                dense
                label="Username"
                append-icon="mdi-account-outline"
                :rules="requiredRule">
              </v-text-field>
              <v-text-field
                v-model="userInfo.password"
                outlined
                dense
                label="Password"
                :type="showPassword ? 'text' : 'password'"
                :append-icon="showPassword ? 'mdi-lock-open-outline' : 'mdi-lock-outline'"
                @click:append="showPassword = !showPassword"
                :rules="requiredRule">
              </v-text-field>

              <v-btn
                type="submit"
                depressed
                rounded
                class="brand-color px-10 mt-3"
                :loading="loading">
                SIGN IN
              </v-btn>
            </v-form>
          </v-card-text>
        </v-card>

        <div class="mx-15 text-center">
          <ErrorsAlert :show-error-msg="hasError" :error-msg="errorMessage"/>
        </div>
      </div>
      <div class="d-flex align-center justify-center rounded-0 login-side-bg">
        <div class="white--text text-center">
        <h1>Hello There</h1>
        <p>Start your journey with us!</p>
        </div>
      </div>
    </v-card>
  </div>
</template>

<script lang="ts">
  import { Component, Vue } from 'vue-property-decorator'
  import { requiredRule } from '~/utils/FormValidation'

  @Component({})
  export default class LoginPage extends Vue {
    valid: boolean = false;
    showPassword: boolean = false;
    loading: boolean = false;
    hasError: boolean = false;
    userInfo: any = {};
    errorMessage: string = "";
    requiredRule: any = [ requiredRule("Item is required") ];
    
    async login() {
      this.hasError = false;
      const form = this.$refs.form as any;
      if(form.validate()) {
        this.loading = true;
        await this.$auth.loginWith('local', {
          data: {
            email: this.userInfo.email,
            password: this.userInfo.password
          }
        }).then((res) => {
          this.loading = false;
        }).catch((err) => {
          if (err.response) {
            let message = "";
            Object.keys(err.response.data).forEach(key => {
              if(Array.isArray(err.response.data[key])) {
                for (var val of err.response.data[key]) {
                  message+= val + "<br>";
                }
              } else {
                message+= err.response.data[key] + "<br>";
              }
            });

            this.loading = false;
            this.hasError = true;
            this.errorMessage = message;
          }
        })
      }
    }
  }
</script>
