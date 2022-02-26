<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    show() {
      console.log(`点击了 ` + this.count , '次')
    }
  },
  mounted () {
    console.log('ButtonCounter');
    
  }
}
</script>

<template>
    <button @click="count++;show()">点击了 {{ count }} 次</button>  
</template>