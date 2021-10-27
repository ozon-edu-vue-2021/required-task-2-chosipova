<template>
  <div>
    <div 
      v-for="(child, i) in children" 
      :key="`${child.name}-${i}`"
      >
      <directory 
        v-if="child.contents && child.contents.length > 0 && child.type === 'directory'"
        :name="child.name"
        :type="child.type"
        :contents="child.contents"
        />
      <file 
      v-else 
      :name="child.name"
      :type="child.type"
      :target="child.target"
      ></file>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TreeChildren',
    beforeCreate: function(){
      this.$options.components.Directory = require("../Directory/Directory.vue").default;
      this.$options.components.File = require("../File/File.vue").default;
    },
    props: {
      children: {
        type: Array,
        default: () => ([])
      }
    }
  }
</script>