<template>
  <div class="container">
    <transition name="pop-up">
      <finished-alert v-if="showFinishedAlert" @closeEvent="closeAlert"></finished-alert>
    </transition>
    <transition name="fade">
      <div class="app-header" v-if="showHeader">
        <h1>  My today TO DO list</h1>
        <button class="add-task__button" type="button" @click="showInput = !showInput">
          <i class="fa fa-plus"> </i>
        </button>
      </div>
    </transition>
    <transition name="show-input">
      <div class="add-task__container" v-if="showInput">
        <label for="task-input">Name</label>
        <div class="input__container">
          <input type="text" v-model="task.name" :class="{'add-task__input': true, 'invalid__input': invalidInput }" id="task-input" placeholder="Task name" @keyup.enter="addTask()">
          <p v-if="invalidInput" class="invalid_info">Enter task name!</p>
        </div>
        <button type="button" @click="addTask()" class="primary__button">Add!</button>
      </div>
    </transition>
    <div class="drag">
      <draggable v-model="tasks" class="dragArea tasks__list" :options="{group:'tasks'}">
        <transition-group name="move-item">
          <div v-for="(task, index) in tasks" :key="index" class="list-item">
            {{task.name}}
            <button class="icon__button add_button" type="button" @click="addToFinished(task, index)"> <i class="fa fa-check" style="color: #44d444"></i></button>
            <button class="icon__button remove_button" type="button" @click="removeFromList(index)"> <i class="fa fa-trash" style="color: #FF6542"></i></button>
          </div>
        </transition-group>
      </draggable>

      <h2>Done</h2>
      <draggable v-model="finished" class="dragArea" :options="{group:'tasks'}">
        <transition-group name="move-item">
          <div v-for="(task, index) in finished" class="list-item item__done" :key="index">{{task.name}}</div>
        </transition-group>
      </draggable>
    </div>
  </div>
</template>

<script>
import finishedAlert from './finishedAlert';
export default{
  components: {
    finishedAlert
  },
  data: () => ({
    showHeader: true,
    tasks: [
      {
        name: 'Work hard'
      },
      {
        name: 'Play hard'
      },
      {
        name: 'Finally get out of bed'
      },
      {
        name: 'Check for new JS framework'
      },
      {
        name: 'Make a lot of money'
      },
    ],
    finished: [
      {
        name: 'Eat dinner'
      }
    ],
    task: {
      name: ''
    },
    showInput: false,
    invalidInput: false,
    showFinishedAlert: false,
  }),
  watch: {
    'task.name'(input) {
      input.length > 0 ? this.invalidInput = false : this.invalidInput = true;
    },
    tasks(taskArr) {
      taskArr.length == 0 ? this.showFinishedAlert = true : this.showFinishedAlert = false;
    },
    showInput(value){
      value ? '' : this.invalidInput = false;
    }
  },
  methods: {
    addToFinished(task, index){
      this.finished.push(task);
      this.tasks.splice(index, 1);
    },
    validateInput(task){
      if(task.name.length > 0){
        return true;
      }
      else{
        return false;
      }
    },
    addTask(){
      let tempTask = JSON.parse(JSON.stringify(this.task));
      if(this.validateInput(tempTask)){
        this.tasks.unshift(tempTask);
        this.showInput = false;
        this.task.name = '';
        this.invalidInput = false;
      }
      else{
        this.invalidInput = true;
      }
    },
    removeFromList(index){
      this.tasks.splice(index, 1);
    },
    closeAlert(){
      this.showFinishedAlert = false;
    }
  }
}
</script>
<style scoped>



</style>
