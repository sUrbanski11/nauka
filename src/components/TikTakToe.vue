<template>
  <div class="wrap">
    <p>Move player {{player}}</p>
      <div class="row" v-for="(b,i) in board" :key="i">
        <div  class="cell" v-for="(k,j) in b" :key="j" @click="move(i,j)">{{k}}</div>
      </div>
      <p v-if="win">Win player {{player === "X" ? "O" : "X"}}</p>
      <p v-else-if="moveCount === 9">Remis</p>
      <button @click="reset">Reset</button>
  </div>
</template>

<script>
export default {
  name:"TikTakToe",
  data(){
    return{
      board:[["","",""],["","",""],["","",""],],
      player: "X",
      moveCount:0,
      win:false
    }
  },
  methods:{
    move(x,y){
      if(!this.board[x][y] && !this.win){
        const newBoard = [...this.board]
        newBoard[x][y] = this.player
        this.board = newBoard
        this.player = this.player === "X" ? "O" : "X"
        this.moveCount += 1

      }
    },
    reset(){
      this.board =[["","",""],["","",""],["","",""],],
      this.player = "X",
      this.moveCount = 0,
      this.win = false
    },
    checkIsWinInRow(){
      for(let i=0;i<=2;i++){
        const [c1,c2,c3] = this.board[i]

        if(c1 && c1 === c2 && c1 === c3){
          return true
        }
      }
      return false;
    },
    checkIsWinInColumn(){
      for(let i=0;i<=2;i++){
        const c1 = this.board[0][i]
        const c2 = this.board[1][i]
        const c3 = this.board[2][i]

        if(c1 && c1 === c2 && c1 === c3){
          return true
        }
      }
      return false;
    },
    checkIsWinInSlant(){
      const index = [0,1,2]
      for(let i=0;i<2;i++){
        const c1 = this.board[0][index[0]]
        const c2 = this.board[1][index[1]]
        const c3 = this.board[2][index[2]]
        index.reverse()
        if(c1 && c1 === c2 && c1 === c3){
          return true
        }
      }
      return false;
    },
  },
  watch:{
    board(){
      this.win = this.checkIsWinInRow() || this.checkIsWinInColumn() || this.checkIsWinInSlant()
    }
  }

}
</script>

<style scoped>
.cell{
  width:75px;
  height: 75px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
}
.row{
    display: flex;
}
.wrap{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>