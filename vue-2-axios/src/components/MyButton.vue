<template>
    <button @click="onClick">MyButton</button>
</template>

<script lang="ts">
    import {Component, Vue} from "vue-property-decorator";
    import axios from 'axios';

    @Component
    export default class MyButton extends Vue{
        public async onClick(){
            console.log('取得 [ 開始 ]');
            await axios
                .get(`/WeatherForecast`)
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (response) {
                    console.log(response);
                });
            console.log('取得 [ 終了 ]');
        }
    }
</script>