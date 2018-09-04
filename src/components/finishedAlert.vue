<template>
<div class="alert__container">
  <div class="alert__message">
    <button type="button" class="close__button" @click="closeAlert()"> <i class="fa fa-times"></i></button>
    <div class="alert__text">
      <h1>Yay! You did it!</h1>
      <img class="alert__image" src="../assets/great-job.png" />
      <h3>You have completed all tasks for today! Good job! :) </h3>
      <h5>Add some more if you still have things to! </h5>
    </div>
  </div>
</div>
</template>
<script>
export default{
  methods: {
    closeAlert() {
      this.$emit('closeEvent')
    }
  }
}
</script>
