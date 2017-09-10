<template lang="html">
  <div class="container">
    <div class="row-master">
      <div class="row1">
        <div class="container-offset-10">
          <!-- <button type="button" name="button" class="btn-warning glyphicon glyphicon-pencil"> Add Task</button> -->
              <!-- Modal content-->
          <div>
              <!-- Trigger the modal with a button -->
              <button id="create" type="button" class="btn btn-danger glyphicon glyphicon-pencil" data-toggle="modal" data-target="#myModal"> Add Task</button>
              <!-- Modal -->
              <div id="myModal" class="modal fade" role="dialog">
                <div class="modal-dialog">
                  <!-- Modal content-->
                  <div class="modal-content">
                    <div class="modal-header">
                      <button type="button" class="close" data-dismiss="modal">&times;</button>
                      <h4 class="modal-title">New Task</h4>
                    </div>
                    <div class="modal-body">
                      <div class="form-group">
                        <label class="control-label" for="focusedInput">Input Title</label>
                        <input class="form-control" id="focusedInput" type="text" placeholder="Input Title" v-model="title">
                      </div>
                      <div class="form-group">
                        <label for="textArea" class="control-label">Description</label>
                        <div>
                          <textarea class="form-control" id="textArea" v-model="description"></textarea>
                        </div>
                      </div>
                      <div class="form-group">
                        <label class="control-label" for="focusedInput">Point</label>
                        <input class="form-control" id="focusedInput" type="text" v-model="point">
                      </div>
                      <div class="form-group">
                        <label class="control-label" for="focusedInput">Assign To</label>
                        <input class="form-control" id="focusedInput" type="text" placeholder="Assign To" v-model="assign_to">
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-danger" data-dismiss="modal"> Cancel</button>
                      <button type="button" class="btn btn-success" data-dismiss="modal" @click="addTask"> Save</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
        </div>
      </div><br>
      <div class="row-2">
        <div class="col-md-3">
          <log></log>
        </div>
        <div class="col-md-3">
          <todo></todo>
        </div>
        <div class="col-md-3">
          <div class="panel panel-info">
        <div class="panel-heading">
          <h3 class="panel-title glyphicon glyphicon-play-circle">  Doing</h3>
        </div>
        <div class="panel-body">
          Panel content
        </div>
      </div>
        </div>
        <div class="col-md-3">
          <div class="panel panel-success">
            <div class="panel-heading">
              <h3 class="panel-title glyphicon glyphicon-check">  Done</h3>
            </div>
            <div class="panel-body">
              Panel content
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import log from '@/components/Log'
import todo from '@/components/Todo'
export default {
  components: {
    log,
    todo
  },
  data () {
    return {
      title: '',
      description: '',
      point: 0,
      assign_to: ''
    }
  },
  methods: {
    addTask () {
      this.$db.ref('task/log/').push({
        title: this.title,
        description: this.description,
        point: this.point,
        assign_to: this.assign_to,
        status: 'log'
      })
      this.title = ''
      this.description = ''
      this.point = 0
      this.assign_to = ''
    }
  }
}
</script>

<style lang="css">
</style>
