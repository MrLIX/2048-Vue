<template>
    <div class="game">
        <div class="board">
            <GameCell :number="cell" v-for="cell in cells"></GameCell>
        </div>
        <div class="buttons">
            <div class="info">
                <h3 class="welcomeText">Welcome to 2048!</h3>
                <p class="welcomeText">Your score: {{score}}</p>
            </div>
            <div class="buttonsUp">
                <button class="btn" @click="move('ArrowUp')">
                    <img id="ArrowUp" src="/images/up.png">
                </button>
            </div>
            <div>
                <button class="btn" @click="move('ArrowLeft')">
                    <img id="ArrowLeft" src="/images/left.png">
                </button>
                 <button class="btn" @click="move('ArrowDown')">
                     <img id="ArrowDown" src="/images/down.png">
                 </button>
                 <button class="btn" @click="move('ArrowRight')">
                     <img id="ArrowRight" src="/images/right.png">
                 </button>
            </div>
            <div class="info">
                <a class="welcomeText" href="https://github.com/mrlix" target="_blank">https://github.com/mrlix</a>
            </div>

        </div>
    </div>
</template>
<script>
    import GameCell from "./GameCell";

    export default {
        name: 'GameBoard',
        data() {
            return {
                cells: [],
                score: 0
            };
        },
        methods: {
            init() {
                this.cells = this.shuffle([
                    2, 2, 0, 0,
                    0, 0, 0, 0,
                    0, 0, 0, 0,
                    0, 0, 0, 0
                ]);
            },
            shuffle(arr) {
                for (let i = arr.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [arr[i], arr[j]] = [arr[j], arr[i]];
                }
                return arr;
            },
            addCells() {
                let emptyCells = [];
                this.cells.forEach((cell, index) => {
                    if (cell === 0) {
                        emptyCells.push(index);
                    }
                });
                if (emptyCells.length > 0) {
                    let index = this.shuffle(emptyCells)[0];
                    this.cells[index] = 2;
                } else {
                    let turns = false;
                    for (let i = 0; i < 16; i++) {
                        if (this.checkTurns(i)) {
                            turns = true;
                            break;
                        }
                    }
                    if (!turns) alert('Game Over!')
                }
            },
            checkTurns(i) {
                let v = this.cells[i]
                return v === this.cells[i + 1] || v === this.cells[i - 1] || v === this.cells[i + 4] || v === this.cells[i - 4]
            },
            onkeydown(e) {
                if (['ArrowLeft', 'ArrowRight', 'ArrowUp', 'ArrowDown'].includes(e.code)) {
                    this.move(e.code)
                }
            },
            move(direction) {
                let arr = [];
                for (let k = 1; k <= 4; k++) {
                    this[direction](k, arr)
                }
                this.addBtnClass(direction)
                this.addCells();
                this.$forceUpdate();
            },
            ArrowLeft(k, arr) {
                for (let i = 0; i < 16; i++) {
                    let index = i - 1;
                    if (k === 3 && index >= 0 && i % 4 !== 0 && this.cells[i] !== 0 && this.cells[index] === this.cells[i] && ![i].includes(arr)) {
                        this.cells[index] += this.cells[i];
                        this.score +=this.cells[index];
                        this.cells[i] = 0;
                        arr.push(index);
                    }
                    if (k !== 3 && index >= 0 && i % 4 !== 0 && this.cells[index] === 0) {
                        this.cells[index] = this.cells[i];
                        this.cells[i] = 0;
                    }
                }
            },
            ArrowRight(k, arr) {
                for (let i = 15; i >= 0; i--) {
                    let index = i + 1;
                    if (k === 3 && index < 16 && i % 4 !== 3 && this.cells[i] !== 0 && this.cells[index] === this.cells[i] && ![i].includes(arr)) {
                        this.cells[index] += this.cells[i];
                        this.score +=this.cells[index];
                        this.cells[i] = 0;
                        arr.push(index);
                    }
                    if (k !== 3 && index < 16 && i % 4 !== 3 && this.cells[index] === 0) {
                        this.cells[index] = this.cells[i];
                        this.cells[i] = 0;
                    }

                }


            },
            ArrowUp(k, arr) {
                for (let i = 0; i < 16; i++) {
                    let index = i - 4;
                    if (k === 3 && index >= 0 && this.cells[index] === this.cells[i] && this.cells[i] !== 0 && ![i].includes(arr)) {
                        this.cells[index] += this.cells[i];
                        this.score +=this.cells[index];
                        this.cells[i] = 0;
                    }
                    if (k !== 3 && index >= 0 && this.cells[index] === 0) {
                        this.cells[index] = this.cells[i];
                        this.cells[i] = 0;
                    }
                }

            },
            ArrowDown(k, arr) {
                for (let i = 16; i >= 0; i--) {
                    let index = i + 4;
                    if (k === 3 && index < 16 && this.cells[i] !== 0 && this.cells[index] === this.cells[i] && ![i].includes(arr)) {
                        this.cells[index] += this.cells[i];
                        this.score +=this.cells[index];
                        this.cells[i] = 0;
                    }

                    if (k !== 3 && index < 16 && this.cells[index] === 0) {
                        this.cells[index] = this.cells[i];
                        this.cells[i] = 0;
                    }
                }

            },
            addBtnClass(direction) {
                let btn = document.getElementById(direction);
                btn.className += " effect effect-before";
                setTimeout(() => {
                    btn.className = '';
                },200)
            },
        }
        ,
        created() {
            this.init();
            window.addEventListener('keydown', this.onkeydown)
        }
        ,
        components: {
            GameCell
        }
        ,
        props: {
            GameBoard: {}
        }
    }
</script>
<style>
    .game {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .board {
        display: flex;
        flex-wrap: wrap;
        width: 600px;
        height: 600px;
        background-color: #d0d6da;
        padding: 6px;
        border-radius: 8px;
    }

    .buttons {
        padding: 10px;
        margin: 10px;
        background-color: #d0d6da;
        border-radius: 8px;

    }

    .buttonsUp {
        display: flex;
        justify-content: center;
    }

    .info {
        text-align: center;
    }

    .welcomeText {
        color: #555;
    }

    .effect {
        content: "";
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        -webkit-transform: scale(0.001, 0.001);
        transform: scale(0.001, 0.001);
        overflow: hidden;
    }

    .effect-before {
        -webkit-animation: effect_dylan 0.8s ease-out;
        animation: effect_dylan 0.8s ease-out;
    }

    .btn {
        width: 100px;
        height: 100px;
        background: inherit;
        border: none;
        outline: none;
    }
    .btn img {
        width: 100%;
        height: 100%;
        margin: 5px;
        position: relative;
    }

    @-webkit-keyframes effect_dylan {
        50% {
            -webkit-transform: scale(1.5, 1.5);
            transform: scale(1.5, 1.5);
            opacity: 0;
        }
        99% {
            -webkit-transform: scale(0.001, 0.001);
            transform: scale(0.001, 0.001);
            opacity: 0;
        }
        100% {
            -webkit-transform: scale(0.001, 0.001);
            transform: scale(0.001, 0.001);
            opacity: 1;
        }
    }

    @keyframes effect_dylan {
        50% {
            -webkit-transform: scale(1.5, 1.5);
            transform: scale(1.5, 1.5);
            opacity: 0;
        }
        99% {
            -webkit-transform: scale(0.001, 0.001);
            transform: scale(0.001, 0.001);
            opacity: 0;
        }
        100% {
            -webkit-transform: scale(0.001, 0.001);
            transform: scale(0.001, 0.001);
            opacity: 1;
        }
    }
    @media(max-width: 768px){
        .game {
            flex-direction: column;
        }
    }

</style>
