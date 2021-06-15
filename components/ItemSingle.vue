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
      <div v-if="pos === 'view'">
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
        <v-btn color="deep-purple lighten-2" text @click="reserve"> Buy </v-btn>
      </div>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  props: {
    item: {
      type: Object,
      default() {
        return {};
      },
    },
    pos: String,
  },
  methods: {
    view() {
      console.log("te");
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
