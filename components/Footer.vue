<template>
   <v-layout row class="v-layout">
       <div style="width: auto; padding: 5px">
           <div class="note grey--text">
                <v-icon small color="green" class="icon">mdi-circle-outline</v-icon>
                <span class="text">Passed</span>
                <v-icon small color="red" class="icon">mdi-circle-outline</v-icon>
                 <span class="text">Pending</span>
                <v-icon small color="cyan" class="icon">mdi-circle-outline</v-icon>
                 <span class="text">Approved</span>
               
           </div>
       </div>
   </v-layout>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
    .note{
        border: 1px solid cyan;
        border-radius: 20px;
        justify-content: center;
    }
    .v-layout{
        padding: 5px;
        justify-content: center;
    }
    .column{
        justify-content: center;
    }
    .text{
        font-size: 20px;
    }
    .icon{
        margin-bottom: 5px;
    }
</style>