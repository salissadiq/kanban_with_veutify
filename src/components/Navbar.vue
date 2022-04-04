<template>
     <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        Vuetifi Kanban
      </div>

      <v-spacer></v-spacer>
      <AddBoardBtn />
    </v-app-bar>
</template>

<script>
    import AddBoardBtn from '@/components/AddBoardBtn'
    export default {
        components:{
            AddBoardBtn
        }
    }
</script>