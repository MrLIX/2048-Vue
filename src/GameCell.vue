<template>
    <div :class="'color' + number" class="cell">{{ number || '' }}</div>
</template>
<script>
    export default {
        name: 'GameCell',
        methods: {},
        props: {
            number: ''
        }
    }
</script>
<style>
    .color0 {
        background-color: #ecf0f1;
        color: #fff;
    }

    @keyframes color_change2 {
        from {
            background-color: #ecf0f1;
        }
        to {
            background-color: #1abc9c;
        }
    }

    .color2 {
        background-color: #1abc9c;
        color: #fff;
        animation-name: color_change2;
        animation-duration: 0.20s;
        animation-direction: alternate;
    }

    @keyframes color_change4 {
        from {
            background-color: #1abc9c;
        }
        to {
            background-color: #2ecc71;
        }
    }

    .color4 {
        animation-name: color_change4;
        background-color: #2ecc71;
        color: #fff;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change8 {
        from {
            background-color: #2ecc71;
        }
        to {
            background-color: #3498db;
        }
    }

    .color8 {
        animation-name: color_change8;
        background-color: #3498db;
        color: #fff;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change16 {
        from {
            background-color: #3498db;
        }
        to {
            background-color: #9b59b6;
        }
    }

    .color16 {
        animation-name: color_change16;
        background-color: #9b59b6;
        color: #fff;
        font-size: 60px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change32 {
        from {
            background-color: #9b59b6;
        }
        to {
            background-color: #34495e;
        }
    }

    .color32 {
        animation-name: color_change32;
        background-color: #34495e;
        color: #fff;
        font-size: 60px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change64 {
        from {
            background-color: #34495e;
        }
        to {
            background-color: #d2a50f;
        }
    }

    .color64 {
        animation-name: color_change64;
        background-color: #d2a50f;
        color: #fff;
        font-size: 60px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change128 {
        from {
            background-color: #d2a50f;
        }
        to {
            background-color: #e67e22;
        }
    }

    .color128 {
        animation-name: color_change128;
        background-color: #e67e22;
        color: #fff;
        font-size: 56px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change256 {
        from {
            background-color: #e67e22;
        }
        to {
            background-color: #e74c3c;
        }
    }

    .color256 {
        animation-name: color_change256;
        background-color: #e74c3c;
        color: #fff;
        font-size: 56px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change512 {
        from {
            background-color: #e74c3c;
        }
        to {
            background-color: #95a5a6;
        }
    }

    .color512 {
        animation-name: color_change512;
        background-color: #95a5a6;
        color: #fff;
        font-size: 56px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change1024 {
        from {
            background-color: #95a5a6;
        }
        to {
            background-color: #574b90;
        }
    }

    .color1024 {
        animation-name: color_change1024;
        background-color: #574b90;
        color: #fff;
        font-size: 46px;
        animation-duration: 1s;
        animation-direction: alternate;

    }

    @keyframes color_change2048 {
        from {
            background-color: #574b90;
        }
        to {
            background-color: #303952;
        }
    }

    .color2048 {
        animation-name: color_change2048;
        background-color: #303952;
        color: #fff;
        font-size: 46px;
    }

    .color4096 {
        background-color: #c44569;
        color: #fff;
        font-size: 46px;
    }

    .color8192 {
        background-color: #78e08f;
        color: #000000;
        font-size: 46px;
    }

    .cell {
        width: 23%;
        height: 23%;
        border-radius: 8px;
        border: 1px solid #ccc;
        margin: 1%;
        font-size: 64px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

</style>
