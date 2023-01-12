<template>
    <section class="lista">
        <Form @formData="calcular" />
        <table class="table is-fullwidth">
            <thead>
                <tr>
                    <th>Nome</th>
                    <th>Peso</th>
                    <th>Altura</th>
                    <th>IMC</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <Table v-for="(pessoa, index) in pessoas" :key="index" :pessoa="pessoa" @reset="init" />
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import IPessoa from '~/interface/IPessoa';

export default defineComponent({
    name: 'IndexPage',
    data() {
        return {
            pessoas: [] as IPessoa[]
        }
    },
    created() {
        this.init()
    },
    methods: {
        init() {
            if (localStorage.length == 0) {
                this.pessoas = []
            } else {
                this.pessoas = JSON.parse(localStorage.getItem('pessoa') || '{}')
            }
        },
        calcular(pessoa: IPessoa) {
            this.pessoas.push(pessoa)
            localStorage.setItem("pessoa", JSON.stringify(this.pessoas))
        }
    }
})
</script>

<style scoped>

</style>