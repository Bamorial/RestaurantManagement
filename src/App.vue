<template>
  <div class="flex w-full h-full justify-between gap-2">
    <div
      class="border shadowCustom bg-white border-black border-2 rounded-lg w-full h-[90vh] m-10 pr-8"
    >
      <div class="m-2 w-full h-full grid grid-cols-4 gap-4">
        <div 
          class="h-[70%] w-[90%] border border-black border-2 rounded-md m-4 flex justify-between"
          v-for="(table, index) in tables"
          :class="{isSelected: selectList[index+1]}"
          @click="selected=table;selectList.fill(0); selectList[selected.id]=1; console.log(selectList)"
        >
      <div  class="mt-1 ml-2">
        {{ table.name }}
      </div>
      <div :style="{background: statusColor[table.status] }" class=" mt-1 mr-2 h-6 w-6 border border-black rounded-xl ">

      </div>
      </div>
      </div>
    </div>

    <div
      class="border overflow-scroll shadowCustom bg-white border-black border-2 rounded-lg w-full h-[90vh] m-10"
    >
    <div class="font-mono text-center text-3xl mt-6">
      Table {{ selected.id }}

    </div>
    <div class="font-mono text-center text-lg">
      Status: {{ statusText[selected.status] }}
    </div>
    <div class="font-mono text-center text-lg">
      comanda:
    </div>
    <div class="grid grid-cols-2 ml-10 mt-10">
      <div class="font-mono font-semibold  text-lg">
        Nume
      </div>
      <div class="font-mono font-semibold  text-lg">
        Cantitate
      </div>
    </div>
    <div class="grid grid-cols-2 ml-10 mt-10 font-mono  text-lg"  v-for="order in selected.order">
      <div>
         {{ order.ordName }}
      </div>
      <div>
        {{ order.quantity }}
      </div>

    </div>
   
    </div>
  </div>
  <div class="flex  justify-around sticky bottom-4 ">
      <button @click="changeState(3)" class="shadowCustom h-16 w-40 border border-black border-2 rounded-md bg-white active:shadow-none active:translate-x-1 active:translate-y-1">DONE</button>
      <button v-if="isBucatar" @click="changeState(2)" class="shadowCustom h-16 w-40 border border-black border-2 rounded-md bg-white active:shadow-none active:translate-x-1 active:translate-y-1">READY</button>

    </div>

</template>
<script setup>
import { ref } from 'vue';
import getAll from './TableGetter.js'
const isBucatar=true
const tables = getAll();
let selected=ref(0)
let selectList=Array(tables.length).fill(0)
selectList[selected.id]=1

console.log(selectList)



const statusColor={
  1:'red',
  2:'yellow',
  3:'green',
  4:'yellow'
}
const statusText={
  1:'comanda noua',
  2:'gata de ridicat',
  3:'masa libera',
  4:'yellow'
}

function changeState(index){

  selected.value.status=index
  tables.find((currentTable)=>{
    if(currentTable.id===selected.value.id){
      currentTable.status=index
      selected.value=currentTable
    }
    else{

    }
  })
}







</script>
