<template>
    <div>
        <div class="search_box">
            <v-text-field v-model="search" class="search" label="Search items"></v-text-field>
            <div class="options">
                <v-select
                    v-model="select_categories"
                    class="select categories"
                    :items="items_categories"
                    label="Categories"
                    attach
                    multiple
                    outlined
                ><template v-slot:selection="{ item, index }">
                    <v-chip v-if="index < 2">
                    <span>{{ item }}</span>
                    </v-chip>
                    <span
                    v-if="index === 2"
                    class="grey--text caption"
                    >
                    (+{{ select_categories.length - 2 }} others)
                    </span>
                </template>
                </v-select>
                <v-select
                    v-model="select_sortby"
                    class="select sortby"
                    :items="items_sortby"
                    label="Sort by"
                    outlined
                ></v-select>
            </div>
        </div>
        <div class="items">
            <div v-for="item in filteredList" :key="item.id" class="item">
                <v-icon @click="check_heart($event)" class="icon-fav">mdi-heart-outline</v-icon>
                <img :src=item.picture alt="">
                <span class="_name">{{ item.name }}</span>
                <div class="bottom">
                    <span class="_creator">{{ item.creator }}</span>
                    <span class="_price">{{ item.price }} ETH</span>
                </div>
            </div>
        </div>
    </div>
</template>
<script>

export default {
    data() {
        return {
            select_categories: [],
            items_categories: [
                'Programming',
                'Design',
                'Gaming',
                'Sport',
                'Other',
            ],
            select_sortby: [],
            items_sortby: [
                'Recent',
                'Oldest',
                'Most Favorited',
                'Lowest Price',
                'Highest Price',
            ],
            items: [],
            search: '',
        }
    },
    methods: {
        check_heart(e) {
            e.innerText = "mdi-heart";
            console.log(e);
        }
    },
    computed: {
        filteredList() {
            return this.items.filter(post => {
                return post.name.toLowerCase().includes(this.search.toLowerCase())
            })
        }
    },
    async fetch() {
        try {
        await this.$axios.get(`/api/items`).then((res) => {
            this.items = res.data;
        });
        console.log(this.items);
        } catch (e) {
            console.log(e);
        }
    }
}
</script>
<style lang="scss">
.search_box {
    margin-top: 12px;
    display: flex;
    .options {
        margin-left: auto;
        display: flex;
        .select {
            &.categories {
                max-width: 330px;
                margin-right: 30px;
            }
            &.sortby {
                max-width: 176px;
            }
        }
    }
    .search {
        margin-right: 20px;
        margin-top: 11px;
    }
}

.items {
    display: flex;
    flex-wrap: wrap;
    .item {
        color: #CCC;
        padding: 0 14px 8px 14px;
        width: 260px;
        height: 350px;
        border: 1px solid #5e5e5e5d;
        box-sizing: border-box;
        border-radius: 4px;
        margin: 0 16px 30px 16px;
        display: flex;
        flex-direction: column;
        box-shadow: 1px 1px 9px 2px black;
        background: #1d1d1d;

        ._name {
            font-size: 14px;
            text-align: center;
            font-weight: bold;
            margin: 18px 0 auto 0;
        }

        .bottom {
            display: flex;
            ._creator, ._price {
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
            color: #BA1616;
            justify-content: right;
            width: max-content;
            margin-left: auto;
            cursor: pointer;

            &::after {
                display: none;
            }
        }
    }
}

@media screen and (max-width: 800px) {
    .search_box {
        flex-direction: column;
        .options {
            margin-left: 0;
            .select {
                &.categories {
                    max-width: none;
                }
            }
        }
        .search {
            max-width: none;
            margin-right: 0px;
        }
    }
}

@media screen and (max-width: 500px) {
    .search_box {
        .options {
            flex-direction: column;
            .select {
                &.categories {
                    margin-right: 0px;
                }
                &.sortby {
                    max-width: none;
                }
            }
        }
    }
}

</style>