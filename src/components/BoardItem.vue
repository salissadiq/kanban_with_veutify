<template>
    <v-hover
        v-slot="{ isHovering, props }"
        open-delay="200"
        class="items"
    >
    <v-card outlined class="mb-3" 
        :elevation="isHovering ? 16 : 2"
        :class="{ 'on-hover': isHovering }"
        v-bind="props"
        >
        <v-card-title class="text-subtitle-1 item-title">
        <span>
            Priority: 
            <v-chip
            class="ma-2 font-weight-bold"
            :color="priorityColor"
            :text-color="priorityTxtColor"
            dark
            >
            {{item.priority}}
        </v-chip>
        </span> 
        <v-spacer />
        <span>
            <v-btn class="handle" text :color="clr" icon xs >
            <v-icon >mdi-sort</v-icon>
        </v-btn>
        </span>
        </v-card-title>
        <v-card-text class="item-body">
            {{item.title}}
        </v-card-text>
        <v-card-actions class="item-footer">
        <v-spacer />
        <v-btn @click="deleteItem" text outlined rounded left color="red">
        Delete
        </v-btn>
        </v-card-actions>
        </v-card >
    </v-hover>
</template>

<script>
    import EventBus from '@/utils/EventBus'
    export default {
        props:['item', 'clr', 'itemIndex', 'boardIndex'],
        computed: {
            priorityColor(){
                if(this.item.priority == 'High') return '#FFCDD2'
                if(this.item.priority == 'Medium') return '#7bf4d0'
                if(this.item.priority == 'Low') return '#e18cf2'

            },
            priorityTxtColor(){
                if(this.item.priority == 'High') return 'red'
                if(this.item.priority == 'Medium') return 'green'
                if(this.item.priority == 'Low') return 'purple'
            }

        },
        data:()=>({

        }),
        methods:{
            deleteItem(){
                EventBus.$emit('deleteItem', {boardIndex: this.boardIndex, itemIndex:this.itemIndex})
            }
        }
        
    }
</script>

<style scoped>
    .item-title{
        padding:0 10px;
    }
    .item-body{
        padding:0 10px;
    }
    .item-footer{
        padding: 4px;
    }
</style>
