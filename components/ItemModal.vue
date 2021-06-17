<template>
  <div class="modal_backdrop">
    <div class="modal">
      <div class="modal_header">
        <h2>Create Item</h2>
        <v-btn icon @click="close">
          <v-icon class="icon _account">mdi-close</v-icon>
        </v-btn>
      </div>
      <ItemForm class="form_user" @submitItem="putItem($event)"></ItemForm>
    </div>
  </div>
</template>

<script>
import ItemForm from "./ItemForm.vue";
export default {
  components: { ItemForm },
  methods: {
    close() {
      this.$emit("close");
    },
    async putItem(item) {
      try {
        await this.$axios.post(`/api/items`, item).then(() => {
          this.$router.push({ name: "index" });
          this.close();
        });
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

<style lang="scss">
.modal_backdrop {
  z-index: 5;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal {
  background: #1e1e1e;
  overflow-x: auto;
  min-width: 500px;
  display: flex;
  flex-direction: column;
  border-radius: 5px;

  .modal_header {
    padding: 15px;
    justify-content: right;
    display: flex;
    border-radius: 0;
    border: 0;

    h2 {
      margin: 0 auto;
      padding-left: 15px;
    }
    .btn_close {
      float: right;
      padding: 0 4px;
      font-weight: bold;
      cursor: pointer;
    }
  }

  .form_user {
    padding: 20px;
  }
}
</style>