<template>
    <div class="field lista">
        <label class="label">Name</label>
        <input class="input" type="text" v-model="name">
        <label class="label">Peso</label>
        <input class="input" type="number" v-model="peso">
        <label class="label">Altura</label>
        <input class="input" type="number" v-model="altura">
        <label class="label">IMC</label>
        <input class="input" type="text" v-model="imc" disabled>
        <div>
            <RouterLink to="/create">
                <Buttons nome="arrow_back" class="button is-success" />
            </RouterLink>
            <Buttons nome="check" @clicado="edit" class="button is-success" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import IPessoa from '~/interface/IPessoa';

export default defineComponent({
    name: "EditPage",
    data() {
        return {
            localData: [] as IPessoa[],
            pessoaEdit: {},
            name: "",
            altura: 0,
            peso: 0,
            imc: 0,
            empty: false
        };
    },
    created() {
        this.filedInput();
    },
    methods: {
        filedInput() {
            this.localData = JSON.parse(localStorage.getItem("pessoa") || "{}");
            this.localData.forEach((data: any) => {
                if (data.id == this.$route.params.id) {
                    this.name = data.nome;
                    this.altura = data.altura;
                    this.peso = data.peso;
                    this.imc = data.imc
                }
            });
        },
        edit() {
            this.localData.forEach((data: any) => {
                if (data.id == this.$route.params.id) {
                    data.nome = this.name;
                    data.altura = this.altura;
                    data.peso = this.peso;
                    data.imc = Math.floor(this.peso / (this.altura * this.altura));
                    localStorage.setItem("pessoa", JSON.stringify(this.localData));
                    this.$router.push("/create");
                }
            });
        }
    }
})
</script>