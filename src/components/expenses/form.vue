<script>
    import {QBtn, QInput} from 'quasar'
    
    export default {
        components: {QBtn, QInput},
        data () {
            return {
                expenses: {
                    amount: '',
                    description: '',
                    date: ''
                }
            }
        },
        methods: {
            submit () {

            }
        }
    }
</script>
<template>
    <form @submit.prevent="submit">
        <q-input class="my-input" type="number" v-model="expenses.amount" placeholder="R$" />
        <q-input class="my-input" type="text" v-model="expenses.description" placeholder="Descrição" />
        <q-input class="my-input" type="datetime" v-model="expenses.date" placeholder="Data" />
        <q-btn color="primary" class="my-button">Salvar</q-btn>
    </form>
</template>
<style scoped>
    my-input{
        margin-bottom: 20px;
    }
    my-button{
        width: 100%;
    }
</style>