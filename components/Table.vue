<template>
    <tbody>
        <tr>
            <td>{{ pessoa.nome }}</td>
            <td>{{ pessoa.peso }}</td>
            <td>{{ pessoa.altura }}</td>
            <td>{{ pessoa.imc }}</td>
            <td>
                <Buttons nome="edit" @clicado="edit" class="button is-warning" />
                ||
                <Buttons nome="delete" @clicado="remove" class="button is-danger" />
            </td>
        </tr>
    </tbody>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import { RouterLink } from 'vue-router';
import IPessoa from '~/interface/IPessoa';

export default defineComponent({
    name: "TableVue",
    data() {
        return {
            localData: [] as IPessoa[]
        };
    },
    props: {
        pessoa: {
            type: Object as PropType<IPessoa>,
            required: true
        }
    },
    methods: {
        edit() {
            this.$router.push(`/edit${this.pessoa.id}`);
        },
        remove() {
            this.$router.push(`/remove${this.pessoa.id}`);
        }
    },
    components: { RouterLink }
});
</script>