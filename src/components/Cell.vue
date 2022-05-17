<template>
  <div class="cell" @click="move">
    <img :src="path" alt="">
  </div>
</template>

<script>
import cross from '@/assets/cross.svg'
import nought from '@/assets/nought.svg'

export default {
  props: [
      'player',
      'index',
      'value',
      'board'
  ],
  methods: {
    move() {
      if (this.value === 'void') {
        this.$emit('move', this.index)
      }
    }
  },
  computed: {
    path() {
      return this.value === 'cross' ? cross : this.value === 'nought' ? nought : null
    }
  }
}
</script>

<style scoped>
.cell {
  background: #0f0f0f50;
  aspect-ratio: 1 / 1;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: 50ms linear;
}

.cell:hover {
  filter: invert(100%);
}
</style>