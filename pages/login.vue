<template>
  <v-app id="inspire">
    <v-main>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="primary">
                <v-toolbar-title>Login form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form
                  ref="form"
                  v-model="valid"
                >
                  <v-text-field
                    name="login"
                    v-model="login.email"
                    :rules="login.emailRules"
                    label="Login"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    id="password"
                    name="password"
                    v-model="login.password"
                    :rules="login.passwordRules"
                    label="Password"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-btn color="primary" to="/register">Register</v-btn>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="userLogin">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      valid: true,
      login: {
        email: '',
        emailRules: [
          v => !!v || 'email is required',
        ],
        password: '',
        passwordRules: [
          v => !!v || 'Password is required',
        ]
      }
    }
  },
  methods: {
    async userLogin() {
      if (this.$refs.form.validate()) {
        try {
          await this.$auth.loginWith('laravelJWT', {
            data: {
              email: this.login.email,
              password: this.login.password
            }
          }).then(() => {
            this.$router.push({
              path: '/'
            })
          })
        } catch (e) {
          console.log(e);
        }
      }
    }
  }
};
</script>
