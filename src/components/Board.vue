<template>
  <div>
    <div v-if="winner">Winner is :{{ winner }}</div>
    <div v-else>Next player: {{ xIsNext ? "X" : "Y" }}</div>
    <div>
      <div class="board">
        <Square
          v-for="(value, index) in squares"
          :key="index"
          :value="value"
          :on-click="() => handleClick(index)"
        />
      </div>
    </div>
  </div>
</template>
<script>
import Square from "./Square.vue";

const calculateWinner = (squares) => {
  const lines = [
    [0, 1, 2], // index of array
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
};

export default {
  name: "Board",
  components: {
    Square,
  },
  data() {
    return {
      squares: Array(9).fill(null),
      xIsNext: true,
      winner: null,
    };
  },
  methods: {
    handleClick(i) {
      if (this.winner) {
        return;
      }
      const squares = [...this.squares];
      if (squares[i]) {
        return;
      }
      squares[i] = this.xIsNext ? "X" : "O";
      this.squares = squares;
      const w = calculateWinner(squares);
      if (w) {
        this.winner = w;
      }
      this.xIsNext = !this.xIsNext;
    },
  },
};
</script>
<style>
.board {
  display: flex;
  width: 300px;
  flex-wrap: wrap;
}
</style>
