<template>
    <v-container>
        <v-layout
                text-center
                wrap
        >
            <v-flex xs12>
                <v-img
                        :src="require('../assets/logo.svg')"
                        class="my-3"
                        contain
                        height="200"
                ></v-img>
            </v-flex>

            <v-flex mb-4>
                <h1 class="display-2 font-weight-bold mb-3">
                    Welcome to Vuetify
                </h1>
                <p class="subheading font-weight-regular">
                    For help and collaboration with other Vuetify developers,
                    <br>please join our online
                    <a href="https://community.vuetifyjs.com" target="_blank">Discord Community</a>
                </p>
            </v-flex>

            <v-flex
                    mb-5
                    xs12
            >
                <v-btn @click.stop="showScheduleForm=true" color="accent" large>
                    Yes
                </v-btn>
                <ScheduleForm v-model="showScheduleForm"/>

                <SearchText :values="company" @choose-value="chooseResult" name="公司" type="company"></SearchText>
                {{company}}
                <SearchText @choose-value="chooseResult" name="名字" type="name"></SearchText>
                {{name}}
            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>
    import ScheduleForm from "./ScheduleForm"
    import SearchText from "./SearchText";

    export default {
        components: {
            SearchText,
            ScheduleForm,
        },
        data: () => ({
            company: 'de',
            name: 'name',
            showScheduleForm: false,
        }),
        methods: {
            chooseResult: function (type, value) {
                eval('this.' + type + "='" + value + "'");
            }
        }
    };
</script>
