<template>
    <v-col cols="4">
        <v-row
        align="end"
        class="fill-height">
            <v-list-item>
                <v-col
                        align-self="start"
                        class="pa-0"
                        cols="12"
                >
                    <v-avatar color="orange" size="162">
                        <span class="white--text headline">{{ name }}</span>
                    </v-avatar>

                    <v-list-item-content>
                        <v-list-item-title class="title">{{name}}</v-list-item-title>
                        <v-list-item-subtitle>{{ gender }}</v-list-item-subtitle>
                    </v-list-item-content>
                </v-col>
            </v-list-item>
        </v-row>
    </v-col>
</template>

<script>
    export default {
        name: "UserInfo",
        props: {
            name: String,
            gender: String
        }
    }
</script>

<style scoped>

</style>