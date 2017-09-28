<script>
    import { QList, QItem, QBtn, Dialog } from 'quasar'
    import { setDone } from '../../persistence/'
    export default {
        components: { QList, QItem, QBtn, Dialog },
        computed: {
            list () {
                return this.$store.state.Expenses.list
            }
        },
        methods: {
            remove (expense) {
                this.$store.commit('REMOVE_EXPENSE', expense)
            },
            askRemove (expense) {
                const self = this
                Dialog.create({
                    title: 'Tem certeza de que deseja remover esta despesa?',
                    // message: '',
                    buttons: [
                        {
                            label: 'Cancelar'
                        },
                        {
                            label: 'Remover',
                            handler () {
                                self.remove(expense)
                            }
                        }
                    ]
                })
            },
            toggle (expense) {
                expense.done = !expense.done
                setDone(expense)
            }
        }
    }
</script>
<template>
    <div class="lista">
        <q-list class="expense" v-for="(expense, index) in list" :key="index" @click="toggle(expense)">
            <q-item :class="{ done: expense.done }">{{ expense.description }}</q-item>
            <q-item :class="{ done: expense.done }"><span>Data: </span> {{ expense.date }}</q-item>
            <q-item :class="{ done: expense.done }"><span>Valor: </span> R$ {{ expense.amount }}</q-item>
            <q-btn @click.prevent="askRemove(expense)" class="full-width" color="red" >Remover</q-btn>
        </q-list>
    </div>
</template>
<style scoped>
.done{text-decoration: line-through; color: #ccc;}
span{font-weight: bold}
.lista{margin-top: 20px;}
.expense{background-color: #E7E9E9; border:2px solid #027be3; padding: 10px; width: 90%; margin:10px auto; cursor: pointer;}
</style>