<template>
    <v-menu offset-y v-model="showMenu">
        <template v-slot:activator="{ on }">
            <v-text-field
                    :label="this.name"
                    @keyup="queryForKeywords()"
                    v-model="this.value"
            ></v-text-field>
        </template>
        <v-list>
            <v-list-tile
                    v-for="(item, index) in suggestKeywords"
                    :key="index"
                    @click="setKeyword('company', 'editedItem.company', index)"
            >
                <v-list-tile-title>{{ item }}</v-list-tile-title>
            </v-list-tile>
        </v-list>
    </v-menu>
</template>

<script>
    export default {
        name: "SearchText",
        props: ['type', 'name', 'value'],
        data: () => ({
            showMenu: false,
        }),
        methods: {
            queryForKeywords: function () {
                let that = this;

                let value = eval('this.' + key);
                if (typeof value == 'undefined') {
                    value = '';
                }
                this.$http.get(process.env.VUE_APP_API_URL + '/friends/suggest/' + type + '/' + encodeURI(value) + '?access-token=100-token')
                    .then(function (response) {
                        that.suggestKeywords = response.data;
                        // console.log(response);

                        if (typeof response.data !== 'undefined' && response.data.length > 0) {
                            that.$nextTick(() => {
                                eval('that.showMenu.' + type + ' = true');
                            });
                        } else {
                            eval('that.showMenu.' + type + ' = false');
                        }
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            },

            setKeyword: function (type, key, index) {
                eval("this." + key + "='" + this.suggestKeywords[index] + "'");
            },
        }
    }
</script>

<style scoped>

</style>