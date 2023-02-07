<template>
    <h1>Secret message</h1>
    <textarea disabled v-bind:value='message' class="input"></textarea>
</template>

<style>
    .input {
        color: #000; 
        border: 2px solid #008CBA;
        border-radius: 8px;
        padding: 6px 6px;
        text-align: left;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
    }
</style>

<script lang="ts">
    import { getMessage } from '../api/api';

    export default {
        data() {
            return {
                message: ''
            }
        },
        async mounted() {
            const params = this.$route.params;
            const secretUrl = params.id;

            if (secretUrl) {
                const resp = await getMessage(secretUrl);
                this.message = resp.text || '';
            }
        }
    }
</script>