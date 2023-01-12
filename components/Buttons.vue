<template>
    <button @click="click">
        <span class="material-symbols-outlined">
            {{ nome }}
        </span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'ButtonsVue',
    emits: ['clicado'],
    props: {
        nome: {
            type: String,
            required: true
        }
    },
    methods: {
        click(): void {
            this.$emit('clicado')
        }
    }
});
</script>