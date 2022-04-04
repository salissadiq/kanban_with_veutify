<template>
    <span>
        <v-btn
                variant="outlined"
                rounded
                outlined
                color="primary"
                @click="dialog=true"
            >
                <v-icon>mdi-plus</v-icon>
                Add Item
            </v-btn>
            <v-btn @click="deleteBoard" icon color="red">
                <v-icon>mdi-trash-can-outline</v-icon>
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
    </span>
</template>

<script>
    import EventBus from '@/utils/EventBus'
    import Modal from '@/components/Modal'
    export default {
        props:['boardIndex'],
        components:{
            Modal
        }, data:()=>({
            dialog: false,
            title: 'Add Board Item',
            labelA: 'Item title',
            labelB: 'Item Priority',
            inputTypeB: 'select'
        }),
        methods:{
            closeDialog(){
                this.dialog = false
            },
            handleSubmit(data){
                EventBus.$emit('addItem',{
                    ...data,
                    boardIndex: this.boardIndex
                })

            },
            deleteBoard(){
              EventBus.$emit('deleteBoard',{boardIndex: this.boardIndex})
            }
        }
    }
</script>