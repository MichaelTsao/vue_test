<template>
    <v-menu offset-y v-model="showMenu.company">
        <template v-slot:activator="{ on }">
            <v-text-field
                    @keyup="queryForKeywords('company', 'editedItem.company', $event)"
                    label="公司"
                    v-model="editedItem.company"
            ></v-text-field>
        </template>
        <v-list>
            <v-list-tile
                    :key="index"
                    @click="setKeyword('company', 'editedItem.company', index)"
                    v-for="(item, index) in suggestKeywords"
            >
                <v-list-tile-title>{{ item }}</v-list-tile-title>
            </v-list-tile>
        </v-list>
    </v-menu>
</template>

<script>
    export default {
        name: "SearchText",
        props: {}
    }
</script>

<style scoped>

</style>