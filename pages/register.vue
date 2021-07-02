<template>
  <v-app id="inspire">
    <v-main>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12">
              <v-toolbar dark color="primary">
                <v-toolbar-title>Register form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form ref="form" v-model="valid">
                  <v-text-field
                    name="email"
                    v-model="register.email"
                    :rules="register.emailRules"
                    label="Login"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    id="password"
                    name="password"
                    v-model="register.password"
                    :rules="register.passwordRules"
                    label="Password"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-btn color="primary" to="/Login">Login</v-btn>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="userRegister">Register</v-btn>
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
      register: {
        email: "",
        emailRules: [(v) => !!v || "Email is required"],
        password: "",
        passwordRules: [(v) => !!v || "Password is required"],
      },
    };
  },

  methods: {
    async userRegister() {
      if (this.$refs.form.validate()) {
        try {
          await this.$axios
            .post("/api/auth/register", {
              email: this.register.email,
              password: this.register.password,
            })
            .then(() => {
              this.$auth.loginWith("laravelJWT", {
                data: {
                  email: this.register.email,
                  password: this.register.password,
                }
              }).then(() => {
                this.$axios.put("/api/users", {
                  name: "User" + Math.floor(Math.random() * 99999),
                  avatar: "https://picsum.photos/500/500",
                }).then(() => {
                  this.$router.push({
                    path: "/",
                  });
                });
              });
            });
        } catch (e) {
          console.log(e);
        }
      }
    },
  },
  auth: false,
};
</script>


