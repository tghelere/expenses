<script>
    import {QBtn, QInput, QCard, QCardMain, QCardTitle, uid} from 'quasar'

    import moment from 'moment'
    
    export default {
        components: {QBtn, QInput, QCard, QCardMain, QCardTitle},
        data () {
            return {
                expense: {
                    id: '',
                    amount: '',
                    description: '',
                    date: moment().format('DD/MM/YYYY'),
                    done: false
                }
            }
        },
        methods: {
            submit () {
                const cloned = JSON.parse(JSON.stringify(this.expense))
                cloned.id = uid()
                this.$store.commit('ADD_EXPENSE', cloned)
                this.reset()
            },
            reset () {
                this.expense.amount = ''
                this.expense.description = ''
                this.expense.date = moment().format('DD/MM/YYYY')
                this.$refs.amount.focus()
            }
        }
    }
</script>
<template>
    <q-card>        
        <q-card-title>
            Nova Despesa
            <span slot="subtitle">Insira sua ultima despesa</span>
        </q-card-title>
        <q-card-main>           
            <form @submit.prevent="submit">
                <q-input ref="amount" class="my-input" type="number" v-model="expense.amount" float-label="Valor R$" />
                <q-input class="my-input" type="text" v-model="expense.description" float-label="Descrição" />
                <q-input class="my-input" type="text" v-model="expense.date" float-label="Data" />
                <q-btn color="primary" class="my-button full-width">Salvar</q-btn>
            </form>
        </q-card-main>
    </q-card>
</template>
<style scoped>
    my-input{
        margin-bottom: 20px;
    }
    my-button{
        margin-top: 20px;
        width: 100%;
    }
</style>