<template>
    <div class="wrapper">
        <div class="header">
            <h1>Secret message </h1>
            <p>Please provide your secret message below</p>
            <div class="header__input-line">
                <textarea v-bind:value='message' v-on:input='textAreaChangeHandler' class="header__input"></textarea>
                <button v-on:click='submitHandler' class="header__btn">Submit</button>
            </div>
            <div v-if='!!secretUrl'>
                <p>Your secret url:</p>
                <div class="header__input-line">
                    <input type='text' disabled v-bind:value='secretUrl'  class="header__input"/>
                    <button v-on:click='goToButtonHandler'  class="header__btn">Go to view content</button>
                </div>
            </div>
        </div>
    </div>

</template>

<style>
    .wrapper {
        margin: 0;
        padding: 0;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .header {}
    .header__input-line {
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .header__input {
        color: #000; 
        border: 2px solid #008CBA;
        border-radius: 8px;
        padding: 6px 6px;
        text-align: left;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
    }
    .header__btn {
        background-color: #008CBA; 
        border: none;
        border-radius: 8px;
        border: 2px solid #008CBA;
        color: white;
        padding: 10px 20px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        transition-duration: 0.4s;
        margin: 0px 10px 0px 10px;
    }
    .header__btn:hover {
        background-color: #fff;
        border: 2px solid #008CBA;
        color: #000;
    }
</style>

<script lang="ts">
    import { postMessage } from '../api/api';

    export default {
        data() {
            return {
                message: '',
                secretUrl: ''
            }
        },
        methods: {
            textAreaChangeHandler(event: any) {
                this.message = event?.target?.value;
            },
            async submitHandler() {
                const resp = await postMessage(this.message);

                if (resp && !!resp.urlGuid) {
                    this.secretUrl = resp.urlGuid;
                }
            },
            goToButtonHandler() {
                this.$router.push({ path: `/${this.secretUrl}` });
            }
        }
    }
</script>
