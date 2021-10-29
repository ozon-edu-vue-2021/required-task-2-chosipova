<template>
  <div class="path">
    <span>{{path}}</span>
  </div>
</template>

<script>
export default {
  name: 'ShowPath',
  props: {
    path: {
      type: String,
      default: '/'
    }
  }
}
</script>

<style scoped>
.path {
  position: fixed;
  top: 0;
  left: 0;
  border-bottom: 1px solid;
  width: 100%;
  background: #fff;
  text-align: center;
  padding: 25px 15px;
}
</style>