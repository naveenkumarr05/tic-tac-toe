<template>
  <div>
    <h1>Welcome to Tic Tac Toe Game</h1>
    <div class="game-point">
      <board :squares="current.squares" @clickSquare="onClickSquare"></board>
      <div class="game-status">
        <div>{{ status }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import Board from "./Board.vue";

export default {
  name: "game",
  components: {
    Board,
  },
  data: () => {
    return {
      history: [
        {
          squares: [],
          position: null,
        },
      ],
      isFirstPlayer: true,
      start: 0,
      status: "",
    };
  },
  computed: {
    current() {
      return this.history[this.start];
    },
    player() {
      return this.isFirstPlayer ? "X" : "O";
    },
    winner() {
      return this.calculateGamer(this.current.squares);
    },
  },
  mounted() {
    this.updateGameStatus();
  },
  methods: {
    onClickSquare(event) {
      this.history = this.history.slice(0, this.start + 1);
      const squares = this.current.squares.slice(
        0,
        this.current.squares.length
      );
      if (this.winner || squares[event.index]) return;
      squares[event.index] = this.player;
      this.history.push({
        squares: squares,
        position: this.getPosition(parseInt(event.index, 10)),
      });
      this.start = this.history.length - 1;
      this.isFirstPlayer = !this.isFirstPlayer;
      this.updateGameStatus();
    },
    updateGameStatus() {
      if (this.winner) {
        this.status = `Player ${this.winner} won!`;
      } else {
        this.status = "Next player: " + this.player;
      }
    },
    calculateGamer(item) {
      const lines = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let line of lines) {
        const [a, b, c] = line;
        if (item[a] && item[a] === item[b] && item[a] === item[c]) {
          return item[a];
        }
      }
      return null;
    },

    /**
     * Get column and row number of a square index
     */
    getPosition(i) {
      let row, col;
      if (i > 5) {
        row = 3;
        col = i - 5;
      } else if (i > 2) {
        row = 2;
        col = i - 2;
      } else {
        row = 1;
        col = i + 1;
      }
      return {
        row,
        col,
      };
    },
  },
};
</script>