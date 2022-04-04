<template>
        <v-card
        max-width="400"
        variant="outlined"
        class="board"
        :style="{borderColor:board.color}"
      >
        <v-card-title>
          <span class="text-h6 mb-1">
            {{board.title}}
          </span>
          <v-spacer />
            <AddItemBtn :boardIndex="boardIndex"/>
        </v-card-title>
        <v-card-text>
            <h4 v-if="board.items.length == 0" class="text-h4 text-center">No Items</h4>
              <div v-else>
                <draggable v-model="board.items" group="items" handle=".handle" >
                    <transition-group transition="scale-transition">
                      <Item 
                      v-for="(item, index) in board.items" 
                      :key="item.title"
                      :item="item"
                      :clr="board.color"
                      :itemIndex="index"
                      :boardIndex="boardIndex"
                  />
                    </transition-group>
                </draggable>
              </div>
        </v-card-text>
      </v-card>
</template>

<script>
import draggable from 'vuedraggable'
import AddItemBtn from '@/components/AddItemBtn'
import Item from '@/components/BoardItem'
    export default {
        components:{
            Item,
            AddItemBtn,
            draggable
        },
        props:['board', 'boardIndex'],
        data:()=>({

        })
    }
</script>

<style scoped>
    .board{
        border-top: 3px solid red;
    }
    .list-move{
      transition: .4s;
    }
</style>