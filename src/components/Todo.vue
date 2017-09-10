<template lang="html">
  <div class="panel panel-primary">
    <div class="panel-heading">
      <h3 class="glyphicon glyphicon glyphicon-edit panel-title">  Todo</h3>
    </div>
    <div class="panel-body ">
    <div class="panel panel-default" v-for="todos in todo">
      <div class="panel-heading">{{ todos.title }}</div>
      <div class="panel-body">
        <p>Point : {{ todos.point }}</p>
        <p>Assign to : {{todos.assign_to }}</p>
        <button type="button" class="btn btn-info" data-toggle="modal" data-target="#myModal2" @click="getData(todos['.key'])">
         Details
        </button>
        <!-- Modal -->
       <div class="modal fade" id="myModal2" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
         <div class="modal-dialog" role="document">
           <div class="modal-content">
             <div class="modal-header">
               <h3 class="modal-title" id="exampleModalLabel">Details task "{{ dataTask.title }}" for {{ dataTask.assign_to }}</h3>
               <button type="button" class="close" data-dismiss="modal">
                 <span aria-hidden="true">&times;</span>
               </button>
             </div>
             <div class="modal-body">
              Task Description: {{ dataTask.description }},
              Task Point: {{ dataTask.point }},
              Status: {{ dataTask.status}}
             </div>
             <div class="modal-footer">
               <button type="button" class="btn btn-danger" data-dismiss="modal" @click="remove(dataTask['.key'])">delete</button>
               <button type="button" class="btn btn-info" data-dismiss="modal" @click="moveToDoing(dataTask['.key'], dataTask.title, dataTask.description, dataTask.point, dataTask.assign_to)">Doing</button>
             </div>
           </div>
         </div>
       </div>
      </div>
     </div>
    </div>
    </div>
  </div>
</div>

</template>

<script>
export default {
  data () {
    return {
      dataTask: {}
    }
  },
  firebase: function () {
    return {
      todo: this.$db.ref('task/todo')
    }
  },
  methods: {
    getData (id) {
      for (let i = 0; i < this.todo.length; i++) {
        if (id === this.todo[i]['.key']) {
          this.dataTask = this.todo[i]
        }
      }
    },
    remove (id) {
      if (window.confirm('delete this task')) {
        this.$db.ref('task/todo/' + id).remove()
      }
    },
    moveToDoing (id, title, description, point, assign) {
      if (window.confirm('move to doing')) {
        this.$db.ref('task/doing').push({
          title: title,
          description: description,
          point: point,
          assign_to: assign,
          status: 'doing'
        })
        this.$db.ref('task/todo/' + id).remove()
      }
    },
    created () {
      this.show()
    }
  }
}
</script>

<style lang="css">
</style>
