<template>
  <form
    class="form_create"
    method="POST"
    @submit.prevent="postItem"
  >
    <label for="name"
      >Name
      <input v-model="name" required />
    </label>
    <label for="picture"
      >Img Url
      <input v-model="picture" required />
    </label>
    <label for="details"
      >Details
      <input v-model="details" required />
    </label>
    <label for="price"
      >Price
      <input v-model="price" type="number" required />
    </label>
    <label for="status"
      >Status
      <input v-model="status" type="status" required />
    </label>
    <h2 v-if="error">
      {{ error }}
    </h2>
    <button type="submit">Submit</button>
  </form>
</template>

<script>
export default {
  props: ['item', 'edit'],
  data() {
    return {
      name: "",
      details: "",
      price: "",
      status: "",
      picture: "",
      error: "",
    };
  },
  methods: {
    postItem() {
      if (
        this.name &&
        this.details &&
        this.price &&
        this.picture &&
        this.status
      ) {
        this.error = "";
        const item = {
          name: this.name,
          details: this.details,
          price: this.price,
          picture: this.picture,
          status: this.status,
        };
        // console.log(item);
        this.$emit("submitItem", item);
      } else {
        this.error = "Missing Fields";
      }
    },
    putItem() {
      this.$emit("submitItem", this.editItem);
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
