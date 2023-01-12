<template>
    <div class="field">
        <label class="label">Name</label>
        <input class="input" type="text" v-model="name">
        <label class="label">Peso</label>
        <input class="input" type="number" v-model="peso">
        <label class="label">Altura</label>
        <input class="input" type="number" v-model="altura">
        <label v-if="empty" class="error">Você não preencheu o necessário</label>
        <div>
            <Buttons nome="check" @clicado="calcular" class="button is-success" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'FromVue',
    data() {
        return {
            name: '',
            altura: 0,
            peso: 0,
            empty: false
        }
    },
    emits: ['formData'],
    methods: {
        calcular() {
            if (this.name === '' || this.peso === 0 || this.altura === 0) {
                this.empty = true
            } else {
                this.$emit('formData', {
                    id: new Date().toISOString().substr(11, 8),
                    nome: this.name,
                    altura: this.altura,
                    peso: this.peso,
                    imc: Math.floor(this.peso / (this.altura * this.altura))
                })
                this.name = ''
                this.altura = 0
                this.peso = 0
                this.empty = false
            }
        }
    }
})
</script>

<style>
.error {
    color: red;
}
</style>