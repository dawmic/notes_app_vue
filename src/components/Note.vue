<template >

      <div draggable="true" class="note" 
        @dragstart="dragAndDrop"
      @dragend="dragEnd"

      >

      <button class="closeBtn" @click="$emit('deleteNote', oneNote.id)">X</button>
      <p class="dateTime">{{oneNote.dateNow}}</p>
      <p class="noteText">{{oneNote.noteText}}</p>
      
    </div>

    
   
  

  
</template>

<script>
export default {
  name: 'Note',
  props: {
    
    oneNote: Object,
    
    
  },
  data(){
    return{
      
    }
  },
  methods:{
     dragAndDrop(e){
       setTimeout(()=>{
        e.target.style.display = "none"; 
       }, 0);
      
    },
    dragEnd(e){
      e.target.style.display = 'block';
    },
      
  },
 
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.note{
  min-height: 200px;
  min-width: 250px;
  max-width: 300px;

   margin: 20px;
   padding: 15px;
 
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  border-radius: 1rem 0 1rem 0;
   /* note card 
   background-color: #FFD723;
   #0E94FF
   #EB2626
  */
 
  
}

.note:nth-child(odd){
  background-color: #0E94FF;
}
.note:nth-child(5n){
  background-color: #EB2626;
}
.closeBtn{
 align-self: flex-end;
 font-weight: 900;
 font-family: sans-serif;
 color: #FAFAFA;
 background-color: transparent;
 border: none;
 outline: non;
 font-size: 1.1rem;
}
.dateTime{
  font-size: 0.8rem;
}
.noteText{
  font-size: 0.9rem;
  font-weight: 500;
}
.emptyInfo{
  font-size: 1.4rem;
  width: 100%;
  text-align: center;
  margin-top: 3rem;
  font-weight: 500;
  animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  backface-visibility: hidden;
  perspective: 1000px; 
}  

p{
  word-wrap: break-word;
  width: 100%;
  color: #FAFAFA;
  background: transparent;
  
}




</style>
