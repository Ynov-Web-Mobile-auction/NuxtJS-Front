<template>
    <div class="search_box">
        <v-text-field class="search" label="Search items"></v-text-field>
        <v-select
            v-model="select_categories"
            class="select categories"
            :items="items_categories"
            label="Categories"
            attach
            multiple
        ><template v-slot:selection="{ item, index }">
            <v-chip v-if="index < 2">
            <span>{{ item }}</span>
            </v-chip>
            <span
            v-if="index === 1"
            class="grey--text caption"
            >
            (+{{ select_categories.length - 1 }} others)
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
        }
    }
}
</script>
<style lang="scss">
.search_box {
    margin-top: 12px;
    display: flex;
    .select {

        &.categories {
            max-width: 20%;
            margin-left: auto;
            margin-right: 30px;
        }

        &.sortby {
            max-width: 10%;
        }
    }
    .search {
        margin-right: 20px;
        max-width: 20%;
    }
}

</style>