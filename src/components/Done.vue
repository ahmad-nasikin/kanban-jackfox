<template lang="html">
  <div class="panel panel-success">
    <div class="panel-heading">
      <h3 class="glyphicon glyphicon glyphicon-edit panel-title">  Done</h3>
    </div>
    <div class="panel-body ">
    <div class="panel panel-default panel-success" v-for="don in done">
      <div class="panel-heading">{{ don.title }}</div>
      <div class="panel-body">
        <p>Point : {{ don.point }}</p>
        <p>Assign to : {{don.assign_to }}</p>
        <button type="button" class="btn btn-success" data-toggle="modal" data-target="#myModal5" @click="getDataDone(don)">
         Details
        </button>
      </div>
     </div>
     <!-- Modal -->
      <div class="modal fade" id="myModal5" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
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
              <button type="button" class="btn btn-info" data-dismiss="modal" @click="moveToDoing(detail['.key'], detail.title, detail.description, detail.point, detail.assign_to)">doing</button>
              <button type="button" class="btn btn-danger" data-dismiss="modal" @click="remove(detail['.key'])">delete</button>
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
      done: this.$db.ref('task/done')
    }
  },
  methods: {
    getDataDone (done) {
      console.log('get data done ', done)
      this.detail = done
    },
    remove (id) {
      if (window.confirm('delete this task')) {
        this.$db.ref('task/done/' + id).remove()
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
        this.$db.ref('task/done/' + id).remove()
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
