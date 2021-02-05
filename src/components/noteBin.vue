<template>
  <div class="bin" @dragover="dragOver"
  @drop="drop"></div>
</template>

<script>
export default {
name: 'NoteBin',
methods:{
    dragOver(){
        console.log('biiin');
    },
    drop(){
        
    },
},
}
</script>

<style scoped>
.bin{
    position: absolute;
    height: 100px;
    width: 100px;
    top: 10%;
    right: 10%;
    border: 2px solid black;
}
</style>