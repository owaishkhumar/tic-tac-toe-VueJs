<template>
    <div class="tic-tac-toe">
        <h1>Tic Tac Toe</h1>
        <div class="board">
            <div v-for="(cell, index) in board" :key="index" class="cell" @click="makeMove(index)">
                {{ cell }}
            </div>
        </div>
        <div class="status">
            <p v-if="winner">Winner: {{ winner }}</p>
            <p v-else-if="isDraw">It's a draw!</p>
            <p v-else>{{ currentPlayer }}'s Turn</p>
        </div>
        <button @click="resetGame">New Game</button>
    </div>
</template>

<script>
export default {
    name: 'TicTacToe',
    data() {
        return {
            board: Array(9).fill(null),
            currentPlayer: 'X',
            winner: null,
        }
    },
    computed: {
        isDraw() {
            return !this.winner && this.board.every(cell => cell !== null)
        }
    },
    methods: {
        makeMove(index) {
            if (this.board[index] === null && !this.winner) {
                this.board[index] = this.currentPlayer
                if (this.checkWinner()) {
                    this.winner = this.currentPlayer
                } else {
                    this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X'
                }
            }
        },
        checkWinner() {
            const lines = [
                [0, 1, 2],
                [3, 4, 5],
                [6, 7, 8],
                [0, 3, 6],
                [1, 4, 7],
                [2, 5, 8],
                [0, 4, 8],
                [2, 4, 6]
            ]
            return lines.some(line => {
                const [a, b, c] = line
                return this.board[a] && this.board[a] === this.board[b] && this.board[a] === this.board[c]
            })
        },
        resetGame() {
            this.board = Array(9).fill(null)
            this.currentPlayer = 'X'
            this.winner = null
        }
    }
}
</script>

<style scoped>
.tic-tac-toe {
    font-family: Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 50px;
}

h1 {
    margin-bottom: 20px;
}

.board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 5px;
    margin-bottom: 20px;
}

.cell {
    width: 100px;
    height: 100px;
    display: flex;
    justify-content: center; 
    align-items: center;
    font-size: 40px;
    font-weight: bold;
    background-color: #f0f0f0;
    cursor: pointer;
}

.status {
    margin:  20px 0;
    font-size: 18px;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background-color: #45a049;
}
</style>