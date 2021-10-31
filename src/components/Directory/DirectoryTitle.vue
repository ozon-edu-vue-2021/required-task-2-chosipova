<template>
  <div
    class="directory-title"
    v-on="$listeners"
  >
    <span>{{ name }}</span>
    <arrow-icon
      :opened="this.$parent.opened"
    />
  </div>
</template>

<script>
export default {
  name: 'DirectoryTitle',
  components: {
      ArrowIcon: () => import('../ArrowIcon/ArrowIcon.vue')
    },
  props: {
    name: {
      type: String,
      default: 'name'
    }
  }
}
</script>

<style scoped>
  .directory-title {
    display: flex;
    align-items: center;
    justify-content: space-between;
    line-height: 1;
    border: 2px solid rgba(0,0,0,0.7);
    padding: 10px 15px;
    border-radius: 6px;
    cursor: pointer;
    user-select: none;
  }
  .directory-title:focus,
  .directory-title:focus-visible {
    border: 2px solid #CE2D4F;
    outline: 0;
  }
</style>