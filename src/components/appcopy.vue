<template>
  <div id="app">
  <h1>Just a notebook.</h1>
    <textarea :class="{errorInfo : error}"
     name="notebook"
      id=""
       cols="30" rows="2"
        v-model="text"
         ref="textarea"
          placeholder="your note">
         
          </textarea>
  
    <button class="submitBtn" @click="addNote">Add note</button>
  <div class="note-container">
 <p v-if="tablica.length < 1" class="emptyInfo">no notes yet 😥</p>
 <div  v-for="item in tablica" v-bind:key="item.id">
    <note 
      @deleteNote="deleteNote"
    :oneNote='item'
    />
    </div>
  </div>   
  </div>
</template>

<script>
import Note from './components/Note.vue'

export default {
  name: 'App',
  components: {
    Note
  },
  data(){
    return{
      text: '',
      error: false,
      
      tablica: [
        {
          noteText: 'This is example note',
         dateNow: new Date(Date.now()).toLocaleString(),
          id: 1,
        }
      ],
    }
  },
  methods:{
    addNote(){
      if(this.text < 1) {
        this.error = true;
        return;
      }
      this.tablica = [{
        noteText : this.text,
        dateNow: new Date(Date.now()).toLocaleString(),
        id: this.tablica.length+1,
}, ...this.tablica];

  this.text = '';
  this.error = false;
  this.$refs.textarea.focus();

  localStorage.setItem('list', JSON.stringify(this.tablica));
},
  deleteNote(id){
    this.tablica = this.tablica.filter(item => item.id !== id);
  },
      
    

  },
  mounted(){
    if (localStorage.getItem('list'))
    this.tablica = JSON.parse(localStorage.getItem('list'));
   
  },
  beforeUpdate(){
    localStorage.setItem('list', JSON.stringify(this.tablica));
  },
  
}
</script>

<style>
*{
  box-sizing: border-box;
   background: #FAFAFA;
  /* color: #cafafe; */
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0 auto;
  color: #2c3e50;

  display: flex;
  flex-direction: column;
 align-items: center;
 width: 90%;
 min-height: 800px;
  
}
h1{
  font-weight: 900;
  font-size: 2.4rem;
  letter-spacing: -2px;
  color: #3D3D3D;
}
h1, textarea, .submitBtn{
  align-self: flex-start;
 
}
/*
.submitBtn{
  width: 16rem;
  background: #FFD723;
  color: black;
  outline: none;
  border: none;
  border-radius: 1rem;
  height: 2.5rem;
  margin: 1rem 0;
  font-weight: 700;
  font-size: 1.1rem;
  transition: all .3s ease-in-out;
 } 
.submitBtn:hover{
  transform: scale(1.05);
}


textarea{
  border: 2px solid #0E94FF;
  border-radius: 0 0 3rem 0;
 font-size: 1.1rem;
 letter-spacing: 2px;
  
  font-family: sans-serif;
  padding: 5px;
}
textarea:focus{
  border: 2px dotted #0E94FF;
  outline: none;
} */
.errorInfo{
  border: 2px solid red;
   animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
  
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
.note-container{
  width: 100%;
  display: flex;
flex-direction: row;
flex-wrap: wrap;
justify-content: flex-start;
align-items: flex-start;  
}




@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }
  
  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}



</style>
