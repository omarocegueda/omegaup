<template>
  <div class="omegaup-course-assignmentlist panel">
    <div class="panel-heading">
      <h3>{{ T.wordsAssignments }}</h3>
    </div>
    <div class="panel-body" v-if="assignments.length == 0">
      <div class="empty-category">{{ T.courseAssignmentEmpty }}</div>
    </div>
    <div class="panel-body" v-else>
      <table class="table table-striped">
        <thead>
          <tr><th v-text="T.wordsHomeworks" colspan="3"></th></tr>
        </thead>
        <tbody>
          <tr v-for="assignment in homeworks">
            <td><a v-bind:href="assignmentUrl(assignment)">{{ assignment.name }}</a></td>
            <td class="button-column"><a v-bind:title="T.courseAssignmentEdit" v-on:click="onEdit(assignment)"><span class="glyphicon glyphicon-edit" aria-hidden="true"></span></a></td>
            <td class="button-column"><a v-bind:title="T.courseAssignmentDelete" v-on:click="onDelete(assignment)"><span class="glyphicon glyphicon-remove" aria-hidden="true"></span></a></td>
          </tr>
        </tbody>
      </table>
      <hr>
      <table class="table table-striped">
        <thead>
          <tr><th v-text="T.wordsTests" colspan="3"></th></tr>
        </thead>
        <tbody>
          <tr v-for="assignment in tests">
            <td><a v-bind:href="assignmentUrl(assignment)">{{ assignment.name }}</a></td>
            <td class="button-column"><a v-bind:title="T.courseAssignmentEdit" v-on:click="onEdit(assignment)"><span class="glyphicon glyphicon-edit" aria-hidden="true"></span></a></td>
            <td class="button-column"><a v-bind:title="T.courseAssignmentDelete" v-on:click="onDelete(assignment)"><span class="glyphicon glyphicon-remove" aria-hidden="true"></span></a></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="panel-footer">
      <form>
        <div class="row">
          <div class="form-group col-md-12">
            <div class="pull-right">
              <button type="submit" class="btn btn-primary" v-on:click.prevent="onNew">
                {{ T.courseAssignmentNew }}
              </button>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    T: Object,
    assignments: Array,
    courseAlias: String,
  },
  data: function() {
    return {
    };
  },
  computed: {
    homeworks: function() {
      return this.assignments.filter((assignment) => {
        return assignment.assignment_type == 'homework';
      });
    },
    tests: function() {
      return this.assignments.filter((assignment) => {
        return assignment.assignment_type == 'test';
      });
    }
  },
  methods: {
    assignmentUrl: function(assignment) {
      return '/course/' + this.courseAlias + '/assignment/' + assignment.alias + '/';
    },
    onDelete: function(assignment) {
      this.$emit('delete', assignment);
    },
    onEdit: function(assignment) {
      this.$emit('edit', assignment);
    },
    onNew: function() {
      this.$emit('new');
    },
  },
};
</script>