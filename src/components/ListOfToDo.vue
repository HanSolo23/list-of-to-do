<template>
  <div class="task__list">
    <div class="task__list__row">
      <Task 
        v-for="(task, index) in todo"
        :key="task.id"
        :task="task"
        :index="index"
      />
    </div>
  </div>
</template>

<script>
import Task from '../components/Task.vue';
import gql from "graphql-tag";

const GET_TASKS = gql`
  query getTasks {
    todo {
      id
      description
      note
      public_date
    }
  }
`;

export default {
  name: 'ListOfToDo',
  components: {
    Task
  },
  data() {
    return {
      todo: [],
    }
  },
  computed: {

  },
  methods: {

  },
  apollo: {
    todo: {
      query: GET_TASKS
    }
  }
}
</script>


<style scoped lang="scss">

.task__list {
  margin-bottom: 20px;
  .task__list__row {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
  
}
</style>
