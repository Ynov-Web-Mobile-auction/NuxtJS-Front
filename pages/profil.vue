<template>
  <v-container fluid>
    <v-layout column>
      <v-card>
        <v-card-text>
          <v-form
            ref="form"
          >
            <v-text-field
              v-model="form.pseudo"
              label="Pseudo"></v-text-field>
            <v-text-field
              v-model="form.bio"
              label="Bio"
            ></v-text-field>
            <v-text-field
              v-model="form.phone"
              label="Phone number"
              type="number"
            ></v-text-field>
            <v-text-field
              v-model="form.address"
              label="Address"
              type="text"
            ></v-text-field>
            <v-text-field
              v-model="form.city"
              label="City"
              type="text"
            ></v-text-field>
            <v-text-field
              v-model="form.zipcode"
              label="Zipcode"
              type="text"
            ></v-text-field>
            <v-text-field
              v-model="form.country"
              label="Country"
              type="text"
            ></v-text-field>
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
        pseudo: '',
        bio: '',
        phone: '',
        created_at: '',
        updated_at: '',
        address: '',
        city: '',
        zipcode: '',
        country: ''
      },
    }
  },

  methods: {
    async updateUser() {
      if (this.$refs.form.validate()) {
        try {
          await this.$axios.put(`/api/users/${this.form.id}`, this.form).then((res) => {
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
