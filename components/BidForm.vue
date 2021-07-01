<template>
  <div>
    <form>
      <v-text-field
        type="number"
        v-model="price"
        :error-messages="priceErrors"
        label="Price in ETH"
        required
        @input="$v.price.$touch()"
        @blur="$v.price.$touch()"
      ></v-text-field>
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
    price: { required },
  },
  data() {
    return {
      price: "",
    };
  },
  computed: {
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
      const bid = {
        price: this.price,
      };
      this.$emit("submitBid", bid);
    },
    clear() {
      this.$v.$reset();
      this.price = "";
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
