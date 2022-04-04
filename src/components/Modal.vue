<template>
    <v-dialog
      v-model="dialog"
      persistent
      width="400"
    >
      <v-card>
          
        <v-card-title>
          <span class="text-h5">{{title}}</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                :label="labelA"
                v-model="inputA"
                :placeholder="`Enter ${labelA}`"
                rounded
                outlined
                dense
                />
              </v-col>
              <v-col cols="12">
                <v-text-field
                v-if="inputTypeB !=='select'"
                v-model="inputB"
                :label="labelB"
                :placeholder="`Enter ${labelB}`"
                :type="inputTypeB"
                rounded
                outlined
                dense
                />
                <v-combobox
                v-else-if="inputTypeB == 'select'"
                v-model="inputB"
                :items="priorities"
                :label="labelB"
                rounded
                outlined
                dense
                chips
                ></v-combobox>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="blue-darken-1"
            text
            @click="handleCloseDialog"
          >
            Close
          </v-btn>
          <v-btn
            color="blue-darken-1"
            text
            @click="submit"
          >
            Save
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
    import EventBus from '@/utils/EventBus'
    export default {
        props:['dialog', 'title', 'labelA', 'labelB', 'inputTypeB'],
        data:()=>({
            priorities: ['High', 'Medium', 'Low'],
            inputA: '',
            inputB: '',
        }),
        methods:{
            submit(){
              this.$emit('submit', {
                inputA: this.inputA,
                inputB: this.inputB,
              })
                this.inputA = '',
                this.inputB = '',
                this.$emit('close')
            },
            handleCloseDialog(){
                this.$emit('close')
            }
        }
    }
</script>