<template>
    <div id="app">
        <div class="container">
            <GameBoard/>
        </div>
    </div>
</template>

<script>

    import GameBoard from "./GameBoard";

    export default {
        name: "app",
        components: {
            GameBoard
        }
    };
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: "Arial";
        font-weight: bold;
    }

    .container {
        margin: 30px auto;
        width: 1200px;
    }
</style>
