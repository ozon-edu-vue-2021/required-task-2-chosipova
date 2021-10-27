<template>
  <svg width="9" height="14" viewBox="0 0 9 14" fill="none" xmlns="http://www.w3.org/2000/svg"
    :class="arrowClasses"
    :opened="opened">
    <path d="M1.99316 12.9865L7.98639 6.99322L1.99316 0.999993" stroke="black" stroke-width="2"
      stroke-linecap="round" stroke-linejoin="round"></path>
  </svg>
</template>

<script>
  export default {
    name: 'ArrowIcon',
    props: {
      opened: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      arrowClasses() {
        return ['icon-arrow', {
          'icon-arrow_down': this.opened
        }];
      }
    }
  }
</script>

<style scoped>
  .icon-arrow {
    transition: 0.3s ease;
  }
  .icon-arrow_down {
    transform: rotate(90deg)
  }
</style>