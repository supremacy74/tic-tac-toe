<template>
  <div class="board">
    <Cell :player="this.player"
          :index="cell.index"
          :value="cell.value"
          :board="board"
          v-for="cell in board"
          @move="move"
    />
  </div>
  <div class="information">
    <button class="button" @click="clear">clear</button>
  </div>
  <div class="end" v-if="visibility.end" @click="visibility.end = false">
    <div class="message">{{ message }}</div>
  </div>
</template>

<script>
import Cell from '@/components/Cell'

export default {
  name: 'Board',
  components: {
    Cell
  },
  data() {
    return {
      cells: Array(9).fill().map((cell, index) => ({ index, value: 'void' })),
      player: 'cross',
      visibility: { end: false },
      message: '',
      moves: 0
    }
  },
  methods: {
    win(index) {

      const variants = [
          [
            [this.board[0], this.board[1], this.board[2]],
            [this.board[3], this.board[4], this.board[5]],
            [this.board[6], this.board[7], this.board[8]]
          ],
          [
            [this.board[0], this.board[3], this.board[6]],
            [this.board[1], this.board[4], this.board[7]],
            [this.board[2], this.board[5], this.board[8]]
          ],
          [
            [this.board[0], this.board[4], this.board[8]],
            [this.board[6], this.board[4], this.board[2]]
          ]
      ]

      for (let i = 0; i < variants.length; i++) {
        for (let j = 0; j < variants[i].length; j++) {
          for (let k = 0; k < variants[i][j].length; k++) {
            if (variants[i][j][k] === this.board[index]) {

              const cell = variants[i][j]

              if (cell[0].value === this.player && cell[1].value === this.player && cell[2].value === this.player) {
                return `The ${this.player} is the winner.`
              }

            }
          }
        }
      }

    },
    move(index) {

      if (this.message === '') {

        this.moves++

        this.cells = this.cells.map(cell => {
          if (cell.index === index) {
            return { index, value: this.player }
          } else {
            return cell
          }
        })

        if (this.moves === 9) {
          this.message = 'Draw.'
        }

        if (this.win(index)) {
          this.message = this.win(index)
        }

        this.player = this.player === 'cross' ? 'nought' : 'cross'

      }

      if (this.message) {
        this.visibility.end = true
      }

    },
    clear() {
      this.cells = Array(9).fill().map((cell, index) => ({ index, value: 'void' }))
      this.moves = 0
      this.message = ''
      this.player = 'cross'
    }
  },
  computed: {
    board() {
      return this.cells
    }
  }
}

</script>

<style scoped>
.board {
  display: grid;
  gap: .5rem;
  grid-template-columns: repeat(3, 5fr);
  grid-template-rows: repeat(3, 5fr);
}

.end {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: #00000050;
  overflow: hidden;
}

.message {
  position: relative;
  z-index: 5;
  top: 40%;
  height: 20%;
  background: #00000095;
  color: #f0f0f0;
  font-size: 125%;
  display: flex;
  justify-content: center;
  align-items: center;
}

@media (min-width: 576px) {
  .message {
    font-size: 3.25rem;
  }
}

.button {
  width: 100%;
  border-radius: 3.25rem;
  font-size: 2.25rem;
  background: #0f0f0f50;
  color: #f0f0f0;
  padding: 5%;
}

.button:hover {
  filter: invert(100%);
}
</style>