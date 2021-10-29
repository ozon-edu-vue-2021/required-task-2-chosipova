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
        :filePath="filePath"
        :parentPath = "parentPath"
        @isSelect="filePath"
        />
      <file 
      v-else 
      :name="child.name"
      :type="child.type"
      :target="child.target"
      :parentPath = "parentPath"
      @isSelect="filePath"
      ></file>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'TreeChildren',
    components: {
      Directory: () => import('../Directory/Directory.vue'),
      File: () => import('../File/File.vue')
    },
    props: {
      children: {
        type: Array,
        default: () => ([])
      },
      parentPath: {
        type: String,
        default: ''
      },
      filePath: {
        type: Function,
        required: true
      }
    }
  }
</script>