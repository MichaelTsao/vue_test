<template>
    <v-dialog max-width="500px" v-model="show">
        <v-card>
            <v-card-actions>
                <v-btn @click.stop="show=false" color="primary" flat>Close</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        props: {
            value: Boolean
        },
        computed: {
            show: {
                get() {
                    return this.value
                },
                set(value) {
                    this.$emit('input', value)
                }
            }
        }
    }
</script>

<style scoped>

</style>