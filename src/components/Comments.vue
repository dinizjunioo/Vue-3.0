<template>
  <div class="container">
    <hr/>
    <div class="form-todo form-group">
      <p>
        <input placeholder="nome" type="text" name="author" class="input" v-model="name" />
      </p>
      <p>
        <input placeholder="comentario"  type="text" name="message" class="input2" v-model="message" >
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>

    <div class="list-group">
      <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
        <span class="comment__author"><strong>Autor: {{comment.name}}</strong></span>
        <p>Comentário: {{comment.message}}</p>
        <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div> 
      </div>
    </div> 
    <hr />
  </div>
</template>

<style>
.input
{
 height: 40px;
    width: 300px;
    padding: 0px 10px 0px 10px;
    border-radius: 5px;
    border: none;
    margin-bottom: 10px;
    background-color: rgb(46, 129, 101);
    color:rgb(181, 205, 226);
    font-size: 15px;
    
}

.input2
{
 height: 80px;
    width: 300px;
    padding: 0px 10px 0px 10px;
    border-radius: 5px;
    border: none;
    margin-bottom: 10px;
    background-color: rgb(46, 129, 101);
    color:rgb(181, 205, 226);
   font-size: 15px;
}

::placeholder
 {
        
        /* Firefox, Chrome, Opera */
        color: rgb(159, 202, 223);
        font-size: 1.5em;
}
</style>

<script>
export default {
  data() {
    return { 
      comments: [],
      name:'',
      message:''
    }
  },
  methods:{
    addComment(){
      if(this.message.trim() === ''){
        return;
      }
      this.comments.push({
        name: this.name,
        message: this.message
      });
      this.name='';
      this.message='';

    },
    removeComment(index){
      this.comments.splice(index,1);
    }
  },
  computed:{
    allComments(){
      return this.comments.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
      }))
    }
  },
  watch:{
    comments (val){
      console.log('val',val)
    }
  }
}

</script>
