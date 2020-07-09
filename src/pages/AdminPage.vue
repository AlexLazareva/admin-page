<template>
    <v-container>
        <v-row class="text-center">
            <!-- Панель пользователя -->
            <UserInfo
                 :name = "userFields[0].label"
                 :gender = "userFields[1].label"
            />
            <!-- Панель пользователя END -->
            <!-- Форма редактирования данных пользователя -->
            <v-col cols="8">
                <v-form>
                    <UserForm v-for="(field, i) in userFields"
                           :key="i"
                           :label="field.label"
                           :type="field.type"
                           :meta="field.meta"
                           userFields="userFields"/>
                    <v-btn
                            :disabled="!valid"
                            color="success"
                            class="mr-4"
                            @click="validate"
                    >
                        Save
                    </v-btn>
                    <v-btn @click="clear">clear</v-btn>
                </v-form>
            </v-col>
            <!-- Форма редактирования данных пользователя END -->
        </v-row>
    </v-container>
</template>

<script>
    import UserForm from "@/components/UserForm";
    import UserInfo from "@/components/UserInfo";
    export default {
        name: "AdminPage",
        components: {
            UserInfo,
            UserForm
        },
        head: {
            meta: [
                { charset: 'utf-8' },
                { name: 'viewport', content: 'width=device-width, initial-scale=1' }
            ]
        },
        data: () => ({
            userFields: [
                {
                    label: "Name",
                    field: "name",
                    type: "string",
                    validator: "nameValidator"
                },
                {
                    label: "Gender",
                    field: "gender",
                    type: "select",
                    validator: "genderValidator",
                    meta: {
                        "values": [
                            {
                                "label": "Male",
                                "value": "male"
                            },
                            {
                                "label": "Female",
                                "value": "female"
                            }
                        ]
                    }
                },
                {
                    label: "Subscription",
                    field: "sub",
                    type: "date",
                    validator: "dateValidator"
                }
            ],
            valid: true
        }),
        methods: {
            validate() {
                console.log("validate");
            },
            clear () {
                console.log("reset");
            }
        }
    }
</script>

<style lang="scss">

</style>