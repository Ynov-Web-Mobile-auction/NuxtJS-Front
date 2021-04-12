<template>
  <v-container fluid>
    <v-layout column>
      <v-card>
        <v-card-text>
          <v-form
              ref="form"
          >
            <v-text-field
                v-model="form.email"
                label="Email"></v-text-field>
            <v-text-field
                v-model="form.name"
                label="Name"></v-text-field>
            <v-text-field
                v-model="form.avatar"
                label="Avatar"></v-text-field>
            <v-text-field
                v-model="form.created_at"
                label="Creation date at"
                type="datetime"
                disabled
            ></v-text-field>
            <v-text-field
                v-model="form.updated_at"
                label="Last update at"
                type="datetime"
                disabled
            ></v-text-field>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" :loading="loading" @click.native="updateUser">
            <v-icon left dark @click="updateUser">mdi-check</v-icon>
            Save Changes
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  pageTitle: 'My Profile',
  data() {
    return {
      loading: false,
      form: {
        id: null,
        email: '',
        name: '',
        avatar: '',
        created_at: '',
        updated_at: '',
      },
    }
  },

  methods: {
    async updateUser() {
      if (this.$refs.form.validate()) {
        try {
          await this.$axios.put(`/api/auth/me`, this.form).then((res) => {
            this.form = res.data;
          });
        } catch (e) {
          console.log(e);
        }
      }
    },
  },
  async fetch() {
    await this.$auth.fetchUser().then((res) => {
      this.form = res.data;
      console.log(this.form);
      console.log(res.data);
    });
  }
}
</script>
