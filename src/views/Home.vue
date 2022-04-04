<template>
  <v-container>
    <h4 v-if="boards.length == 0" class="text-h4 text-center">You don't have any Board Yet!!</h4>
    <div v-else class="board-container">
      <Board 
        v-for="(board, index) in boards"
        :key="index"
        :board="board"
        :boardIndex="index"
        />
    </div>
  </v-container>
</template>

<script>
import Board from '@/components/Board'
import EventBus from '@/utils/EventBus'
export default {
  name: 'Home',
  components: {
    Board
  },
  data:()=>({
    boards:[]
  }), 
  watch:{
    boards(){
        localStorage.setItem('boards', JSON.stringify(this.boards))
    }
  },
  mounted(){
    const temp = localStorage.getItem('boards')
      if(temp){
          this.boards = JSON.parse(temp) || this.boards
      }
    EventBus.$on('addBoard', (data)=>{
      this.boards.push({
        title: data.inputA,
        color: data.inputB,
        items:[]
      })

    })
    EventBus.$on('addItem', (data)=>{
      this.boards[data.boardIndex].items.push({
        title: data.inputA,
        priority: data.inputB
      })
      localStorage.setItem('boards', JSON.stringify(this.boards))
    })
    EventBus.$on('deleteBoard', (data)=>{
      this.boards.splice(data.boardIndex, 1)
    })
    EventBus.$on('deleteItem', (data)=>{
      this.boards[data.boardIndex].items.splice(data.itemIndex, 1)
      localStorage.setItem('boards', JSON.stringify(this.boards))
    })
    EventBus.$on('sortItems', ()=>{
      localStorage.setItem('boards', JSON.stringify(this.boards))
    })
  }
}
</script>
<style scoped>
  .board-container{
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5em;
  }
</style>
