<template>
  <form @submit.prevent="sendForm">
      <textarea name="" id="" cols="30" rows="3"
      ref="textarea"
      placeholder="note..."
      :class="{errorInfo : error}"
      v-model="text"  
        @focus="resetFlag"
        @keypress="resetFlag"
      ></textarea>
     
      <p v-if="error" class="error">note can't be empty</p>
      <p v-if="success" class="success">Added successfully</p>
      <button class="submitBtn">Add note</button>
  </form>
</template>

<script>
export default {
    name: 'NoteForm',
    props:{
        
    },
    data(){
        return{
            text: '',
            error: false,
            success: false,
        }
    },
    methods:{
        sendForm(){
            if(this.text === ''){
                this.error = true;
                this.success = false;
                return;
            }
            this.$emit('sendForm', this.text);
            this.text = '';
            this.$refs.textarea.focus();
            this.error = false;
            this.success = true;
           

        },
        resetFlag(){
        this.error = false;
        this.success = false;
    },
    },
   
}
</script>

<style>
form{
  width: 100%;
  display: flex;
  flex-direction: column;
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
}
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
.errorInfo{
  border: 2px solid red;
   animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
}
.error{
    color: red;

}
.success{
    color: #32A95D;
}
</style>