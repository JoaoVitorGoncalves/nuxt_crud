<template>
    <div class="field lista">
        <label class="label">Name</label>
        <input class="input" type="text" v-model="name" disabled>
        <label class="label">Peso</label>
        <input class="input" type="number" v-model="peso" disabled>
        <label class="label">Altura</label>
        <input class="input" type="number" v-model="altura" disabled>
        <label class="label">IMC</label>
        <input class="input" type="number" v-model="imc" disabled>
        <div>
            <RouterLink to="/create">
                <Buttons nome="arrow_back" class="button is-success" />
            </RouterLink>
            <Buttons nome="check" @clicado="remove" class="button is-danger" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import IPessoa from '~/interface/IPessoa';

export default defineComponent({
    name: 'EditPage',
    data() {
        return {
            localData: [] as IPessoa[],
            pessoaEdit: {},
            name: '',
            altura: 0,
            peso: 0,
            imc: 0,
            empty: false
        }
    },
    created() {
        this.init()
    },
    methods: {
        remove() {
            this.localData.forEach((data: any) => {
                if (data.id == this.$route.params.id) {
                    this.localData.splice(this.localData.indexOf(this.localData[data.id]), 1);
                    localStorage.setItem("pessoa", JSON.stringify(this.localData));
                    this.$router.push("/create");
                }
            });
        },
        init() {
            this.localData = JSON.parse(localStorage.getItem("pessoa") || "{}");
            this.localData.forEach((data: any) => {
                if (data.id == this.$route.params.id) {
                    this.name = data.nome;
                    this.altura = data.altura;
                    this.peso = data.peso;
                    this.imc = data.imc
                }
            });
        }
    }
})
</script>
