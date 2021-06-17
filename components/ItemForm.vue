<template>
  <div>
    <form>
      <v-text-field
        v-model="name"
        :error-messages="nameErrors"
        :counter="10"
        label="Name"
        required
        @input="$v.name.$touch()"
        @blur="$v.name.$touch()"
      ></v-text-field>
      <v-text-field
        v-model="picture"
        :error-messages="pictureErrors"
        label="Picture Url"
        required
        @input="$v.picture.$touch()"
        @blur="$v.picture.$touch()"
      ></v-text-field>
      <v-textarea
        v-model="details"
        :error-messages="detailsErrors"
        :counter="255"
        rows="3"
        label="Details"
        required
        @input="$v.details.$touch()"
        @blur="$v.details.$touch()"
      ></v-textarea>
      <v-text-field
        type="number"
        v-model="price"
        :error-messages="priceErrors"
        label="Price in ETH"
        required
        @input="$v.price.$touch()"
        @blur="$v.price.$touch()"
      ></v-text-field>
      <v-select
        v-model="status"
        :items="items"
        item-text="state"
        item-value="id"
        label="Status"
        required
        @change="$v.status.$touch()"
        @blur="$v.status.$touch()"
      ></v-select>
      <v-btn class="mr-4" @click="submit">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </form>
  </div>
</template>
<script>
import { validationMixin } from "vuelidate";
import { required, maxLength, email } from "vuelidate/lib/validators";

export default {
  mixins: [validationMixin],
  validations: {
    name: { required, maxLength: maxLength(20) },
    picture: { required },
    details: { required, maxLength: maxLength(255) },
    price: { required },
    status: { required },
  },
  data() {
    return {
      name: "",
      details: "",
      price: "",
      status: { state: "Public", id: 1 },
      items: [
        {
          id: 1,
          state: "Public",
        },
        {
          id: 2,
          state: "Private",
        },
      ],
      picture: "",
      error: "",
    };
  },
  computed: {
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push("Name must be at most 20 characters long");
      !this.$v.name.required && errors.push("Name is required.");
      return errors;
    },
    detailsErrors() {
      const errors = [];
      if (!this.$v.details.$dirty) return errors;
      !this.$v.details.maxLength &&
        errors.push("Details must be at most 255 characters long");
      !this.$v.details.required && errors.push("details is required.");
      return errors;
    },
    pictureErrors() {
      const errors = [];
      if (!this.$v.picture.$dirty) return errors;
      !this.$v.picture && errors.push("Must be valid url");
      !this.$v.picture.required && errors.push("Picture is required");
      return errors;
    },
    priceErrors() {
      const errors = [];
      if (!this.$v.price.$dirty) return errors;
      !this.$v.price && errors.push("Must be valid price");
      !this.$v.price.required && errors.push("Price is required");
      return errors;
    },
  },
  methods: {
    submit() {
      this.$v.$touch();
      const item = {
        name: this.name,
        details: this.details,
        price: this.price,
        picture: this.picture,
        status: this.status.id,
      };
      this.$emit("submitItem", item);
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.picture = "";
      this.details = "";
      this.price = "";
      this.status = "";
    },
  },
};
</script>

<style lang="scss">
.form_create {
  display: flex;
  flex-direction: column;

  label,
  select,
  button {
    width: min-content;
    margin: 10px auto;
  }

  label {
    color: #2c3e50;
    font-weight: bold;
    input,
    textarea {
      margin-top: 5px;
      border: 1px solid rgb(158, 158, 158);
      border-radius: 4px;
      padding: 8px 30px;
    }
  }

  button {
    margin-left: auto;
    align-items: center;
    background-color: rgb(32, 129, 226);
    border-radius: 5px;
    color: white;
    cursor: pointer;
    display: inline-flex;
    font-size: 16px;
    font-weight: 600;
    justify-content: center;
    padding: 12px 20px;
    text-align: center;
    user-select: none;
    max-height: 100%;
    border: 1px solid rgb(32, 129, 226);

    &:hover {
      transition: all 0.2s ease 0s;
      box-shadow: rgba(14, 14, 14, 0.25) 0px 0px 8px 0px;
      background-color: rgb(24, 104, 183);
    }
  }

  select {
    background: rgb(255, 255, 255) none repeat scroll 0% 0%;
    color: rgb(14, 14, 14);
    height: 48px;
    padding: 0px 12px;
    border-radius: 5px;
    border: 1px solid rgb(158, 158, 158);
    font-size: 16px;
  }
}
</style>
