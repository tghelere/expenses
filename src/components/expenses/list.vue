<script>
import {QList, QItem} from 'quasar'
    export default {
        components: { QList, QItem },
        computed: {
            list () {
                return this.$store.state.Expenses.list
            }
        }
    }
</script>
<template>
    <div class="lista">
        <q-list class="expense" v-for="(expense, index) in list" :key="index" >
            <q-item>{{ expense.description }}</q-item>
            <q-item><span>Data: </span> {{ expense.date }}</q-item>
            <q-item><span> Valor: </span> R$ {{ expense.amount }}</q-item>
            
        </q-list>
    </div>
</template>
<style scoped>
span{font-weight: bold}
.lista{margin-top: 30px;}
.expense{background-color: #E7E9E9; border:2px solid #027be3}
</style>