<template>
  <div id="app">
    <transition appear name="add-window-animation">
      <AddTask/>
    </transition>
    <transition appear name="tasks-animation">
      <ListOfToDo/>
    </transition> 
  </div>
</template>

<script>
import ListOfToDo from './components/ListOfToDo.vue';
import AddTask from './components/AddTask.vue';

export default {
  name: 'App',
  components: {
    ListOfToDo,
    AddTask
  },
  data() {
    return {
      
    }
  },
  methods: {

  },
}
</script>

<style lang="scss">

body {
  background: url('./assets/1.jpg') 0 0 / cover no-repeat;
  #app {
    overflow: hidden;
    .add-window-animation-enter-active {
      transition: all 1s ease;
    }
    .add-window-animation-enter {
      transform: translateX(-2000px);
    }
    .tasks-animation-enter-active {
      transition: all 1s ease;
    }
    .tasks-animation-enter {
      transform: translateX(2000px);
    }
  }
  
}


</style>
