<template>
  <v-card :class="pos === 'view' ? '_view' : '_buy'" class="item mx-auto my-12">
    <v-img height="230" :src="item.picture"></v-img>

    <v-card-title class="name py-2">{{ item.name }}</v-card-title>
    <v-card-text v-if="pos !== 'view'">{{ item.details }}</v-card-text>

    <div class="bottom">
      <v-card-text class="_creator">{{ item.creator }}</v-card-text>
      <v-card-text class="_price"> {{ item.price }}&nbsp;ETH </v-card-text>
    </div>

    <v-divider class="mx-4"></v-divider>

    <v-card-actions class="btn_view">
      <div v-if="create === 'true'">
        <v-btn color="deep-purple lighten-2" text @click="createauction">
          Create Auction
        </v-btn>
      </div>
      <div v-else-if="pos === 'view'">
        <v-btn
          :to="{ path: '/items?id=' + item.id }"
          color="deep-purple lighten-2"
          text
          @click="view"
        >
          View
        </v-btn>
      </div>
      <div v-else>
        <v-btn color="deep-purple lighten-2" text @click="modalShow = true">
          Buy
        </v-btn>
      </div>
    </v-card-actions>
    <create-bid-modal
      color="deep-purple lighten-2"
      :id_item="item.id"
      v-if="modalShow"
      @close="modalShow = false"
    />
  </v-card>
</template>
<script>
import CreateBidModal from "../components/CreateBidModal.vue";

export default {
  components: {
    CreateBidModal,
  },
  data() {
    return {
      modalShow: false,
      duration: {"duration": "2021-06-14 08:37:10"},
    };
  },
  props: {
    item: {
      type: Object,
      default() {
        return {};
      },
    },
    pos: String,
    create: String,
  },
  methods: {
    view() {
      console.log("te");
    },
    async createauction() {
      try {
        await this.$axios
          .post(`/auctions/${this.item.id}`, this.duration)
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
<style lang="scss">
.item {
  width: 300px;

  &._view {
    height: 400px;

    .name {
      padding-top: 10px !important;
      padding-bottom: 20px !important;
    }
  }

  .name {
    font-size: 16px;
    text-align: center;
    font-weight: bold;
    padding-bottom: 0 !important;

    .highlight {
      color: white;
    }
  }

  .bottom {
    display: flex;
    ._creator,
    ._price {
      font-size: 12px;
    }

    ._creator {
      font-style: italic;
    }

    ._price {
      width: auto;
      margin-left: auto;
    }
  }

  .btn_view {
    justify-content: center;
    font-size: 14px;
  }
}
</style>
