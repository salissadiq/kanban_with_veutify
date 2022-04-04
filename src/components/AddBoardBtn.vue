<template>
    <div>
        <v-btn
        rounded
        dark
        outlined
        @click="dialog=true"
        
      >
        <v-icon>mdi-plus</v-icon>
        <span class="mr-2">Add Board</span>
      </v-btn>
      <Modal 
        :dialog="dialog"
        :title="title"
        :labelA="labelA"
        :labelB="labelB"
        :inputTypeB="inputTypeB"
        @close="closeDialog"
        @submit="handleSubmit"
        />
    </div>
</template>

<script>
import EventBus from '@/utils/EventBus'
import Modal from '@/components/Modal'
    export default {
        components:{
            Modal
        },
        data:()=>({
            dialog: false,
            title: 'Add Board',
            labelA: 'Board title',
            labelB: 'Board color',
            inputTypeB: 'color'
        }),
        methods:{
            handleSubmit(data){
                EventBus.$emit('addBoard', data)
            },
            closeDialog(){
               this.dialog = false;
            }
        }
    }
</script>