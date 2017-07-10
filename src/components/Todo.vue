<template>
  <div>
    <div class='ui centered card'>
        <div class='content'>
            <div class='header'>
                {{ todo.title }}
            </div>
            <div class='meta'>
                {{ todo.project }}
            </div>
            <div class='extra content'>
                <span class='right floated edit icon'>
                <i class='edit icon' v-on:click="showForm"></i>
                </span>
                <span class='right floated trash icon' v-on:click="deleteTodo(todo)">
                <i class='trash icon'></i>
                </span>
            </div>
        </div>  
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Title</label>
          <input type='text' v-model="todo.title" >
        </div>
        <div class='field'>
          <label>Project</label>
          <input type='text' v-model="todo.project" >
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>        
    <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" disabled v-on:click="completeTodo(todo)">
        Completed
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" v-on:click="completeTodo(todo)">
        Pending
    </div> 
     <!-- end of centered card -->
    </div>
    </br>
  </div>
</template>

<script type = "text/javascript" >

// Bon à savoir, c'est le child qui boucle sur les todos, d'où le fait qu'on soit passé à todo singulier
// et qu'on ait retiré la boucle dans ce component
export default {
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    },
    deleteTodo (todo) {
      console.log('clicked')
      this.$emit('delete-todo', todo)
    },
    completeTodo (todo) {
      this.$emit('complete-todo', todo)
    }
  }
}
</script>
