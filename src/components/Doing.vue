<template lang="html">
  <div class="panel panel-info">
    <div class="panel-heading">
      <h3 class="glyphicon glyphicon glyphicon-edit panel-title">  Doing</h3>
    </div>
    <div class="panel-body ">
    <div class="panel panel-default panel-info" v-for="doings in doing">
      <div class="panel-heading">{{ doings.title }}</div>
      <div class="panel-body">
        <p>Point : {{ doings.point }}</p>
        <p>Assign to : {{doings.assign_to }}</p>
        <button type="button" class="btn btn-info" data-toggle="modal" data-target="#myModal4" @click="getDataDoing(doings)">
         Details
        </button>
      </div>
     </div>
     <!-- Modal -->
      <div class="modal fade" id="myModal4" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h3 class="modal-title" id="exampleModalLabel2">Details task "{{ detail.title }}" for {{ detail.assign_to }}</h3>
              <button type="button" class="close" data-dismiss="modal">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
             Task Description: {{ detail.description }},
             Task Point: {{ detail.point }},
             Status: {{ detail.status}}
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-primary" data-dismiss="modal" @click="moveToTodo(detail['.key'], detail.title, detail.description, detail.point, detail.assign_to)">todo</button>
              <button type="button" class="btn btn-danger" data-dismiss="modal" @click="remove(detail['.key'])">delete</button>
              <button type="button" class="btn btn-success" data-dismiss="modal" @click="moveToDone(detail['.key'], detail.title, detail.description, detail.point, detail.assign_to)">done</button>
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
      detail: {}
    }
  },
  firebase: function () {
    return {
      doing: this.$db.ref('task/doing')
    }
  },
  methods: {
    getDataDoing (doings) {
      console.log('get data doing ', doings)
      this.detail = doings
    },
    remove (id) {
      if (window.confirm('delete this task')) {
        this.$db.ref('task/doing/' + id).remove()
      }
    },
    moveToTodo (id, title, description, point, assign) {
      if (window.confirm('move to todo')) {
        this.$db.ref('task/todo').push({
          title: title,
          description: description,
          point: point,
          assign_to: assign,
          status: 'todo'
        })
        this.$db.ref('task/doing/' + id).remove()
      }
    },
    moveToDone (id, title, description, point, assign) {
      if (window.confirm('move to done')) {
        this.$db.ref('task/done').push({
          title: title,
          description: description,
          point: point,
          assign_to: assign,
          status: 'done'
        })
        this.$db.ref('task/doing/' + id).remove()
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
