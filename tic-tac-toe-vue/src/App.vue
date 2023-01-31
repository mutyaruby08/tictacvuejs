<script setup>
import {ref,computed} from 'vue'

const player = ref('X');
const board = ref([
  ['','',''],
  ['','',''],
  ['','',''],
])

const CalcWinner = (squares) => {
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

  for (let i = 0; i < lines.length; i++){
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] 
                   && squares[a] === squares[c])
    {
      return squares[a];
    }
  }
  return null;
}

const winner = computed(() => CalcWinner(board.value.flat()))

const MakeMove = (x,y) => {
  if (winner.value) return
  
  if (board.value[x][y]) return
  
  board.value[x][y] = player.value

  player.value = player.value === 'X' ? 'O' : 'X'
}

const ResetGame = () => {
  board.value = [
  ['','',''],
  ['','',''],
  ['','',''],
  ]
  player.value = 'X'

}
</script>

<template>
  <main class="flex justify-center pt-8 text-center bg-gradient-to-r from-cyan-500 to-blue-500 min-h-screen text-white">
    <div class="h-1/2 w-96 border-t-4 border-r-4 border-b-4 border-l-4 border-white" >
      <br/>
    <h1 class="mb-8 text-3xl font-bold uppercase">Tic Tac Toe</h1>

    <h3 class="text-xl mb-4">Player {{ player }}'s turn</h3>

    <div class="flex flex-col items-center mb-8">
      <div 
        v-for="(row, x) in board"
        :key="x" 
        class="flex">

      <div v-for="(cell, y) in row" 
        :key="y"
        @click="MakeMove(x,y)"
        :class="'border border-white w-20 h-20 hover:bg-white flex items-center justify-center material-icons-outlined text-4x1 cursor-pointer'">
        {{ cell === 'X' ? 'close' : cell === 'O' ? 'circle' : '' }}
      </div>

    </div>
    <br/>
    
    <h2 v-if="winner" class="text-4xl font-bold mb-b">Player '{{ winner }}' wins!</h2>
    <br/>
     <button @click="ResetGame" class="px-4 py-2 bg-red-500 rounded uppercase font-bold hover:bg-pink-600">Reset Game</button>
  </div>
</div>
  </main>


</template>

<style scoped> 
</style>
