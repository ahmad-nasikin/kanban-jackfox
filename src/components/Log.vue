<template lang="html">
  <div class="panel panel-danger">
    <div class="panel-heading">
      <h3 class="glyphicon glyphicon-list-alt panel-title">  Log</h3>
    </div>
    <div class="panel-body">
    <div class="panel panel-default" v-for="logs in log">
      <div class="panel-heading">{{ logs.title }}</div>
      <div class="panel-body">
        <p>Point : {{ logs.point }}</p>
        <p>Assign to : {{logs.assign_to }}</p>
        <button type="button" class="btn btn-info" data-toggle="modal" data-target="#myModal2" @click="getData(logs['.key'])">
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
                 <button type="button" class="btn btn-danger" data-dismiss="modal" @click="deleteTask(dataTask['.key'])">delete</button>
                 <button type="button" class="btn btn-info" data-dismiss="modal" @click="moveToTodo(dataTask['.key'], dataTask.title, dataTask.description, dataTask.point, dataTask.assign_to)">todo</button>
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
      log: this.$db.ref('task/log')
    }
  },
  methods: {
    getData (id) {
      for (let i = 0; i < this.log.length; i++) {
        if (id === this.log[i]['.key']) {
          this.dataTask = this.log[i]
        }
      }
    }
  },
  created () {
    this.show()
  },
  delete (id) {
    this.$db.ref('task/log' + id).remove()
  }
}
</script>

<style lang="css">
</style>
