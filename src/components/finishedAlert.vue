<template>
<div class="alert__container">
  <div class="alert__message">
    <button type="button" class="close__button" @click="closeAlert()"> <i class="fa fa-times"></i></button>
    <h1>YAY! You did it!</h1>
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
