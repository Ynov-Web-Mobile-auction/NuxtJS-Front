<template>
  <div class="item">
    <NuxtLink :to="{ path: '/items?id=' + item.id }">
      <v-icon @click="check_heart($event)" class="icon-fav"
        >mdi-heart-outline</v-icon
      >
      <img :src="item.picture" alt="" />
      <span v-html="item.nameFormated" class="_name">{{
        item.nameFormated
      }}</span>
      <div class="bottom">
        <span class="_creator">{{ item.creator }}</span>
        <span class="_price">{{ item.price }} ETH</span>
      </div>
    </NuxtLink>
  </div>
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
  },
  data() {
    return {};
  },
  methods: {
    check_heart(e) {
      e.innerText = "mdi-heart";
      console.log(e);
    },
  },
};
</script>
<style lang="scss">
.item {
  color: #ccc;
  padding: 0 14px 8px 14px;
  width: 258px;
  height: 350px;
  border: 1px solid #5e5e5e5d;
  box-sizing: border-box;
  border-radius: 4px;
  margin: 0 16px 30px 16px;
  display: flex;
  flex-direction: column;
  box-shadow: 1px 1px 9px 2px black;
  background: #1d1d1d;

  & > a {
    color: inherit !important;
    text-decoration: none;
  }

  ._name {
    font-size: 14px;
    text-align: center;
    font-weight: bold;
    margin: 18px 0 auto 0;

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
      margin-left: auto;
    }
  }

  img {
    max-width: 230px;
    max-height: 230px;
    margin: 0 auto;
    border: #4f4f4f 1px solid;
  }

  .icon-fav {
    padding: 6px 0;
    font-size: 20px;
    color: #ba1616;
    justify-content: right;
    width: max-content;
    margin-left: auto;
    cursor: pointer;

    &::after {
      display: none;
    }
  }
}
</style>
