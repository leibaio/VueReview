<script>
  export default {
    data() {
      return {
        question: '',
        answer: 'Questions usually contain a question mark. ;-'
      }
    },

    watch: {
      // 问题改变，函数将运行
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
        immediate: true //强制积极执行回调
      }
    },

    methods: {
      async getAnswer() {
      this.answer = 'Thinking...'
      try {
        const res = await fetch('http://wtf.api')
        this.answer = (await res.json()).answer
      } catch (error) {
        this.answer = 'Error! Could not reach the API' + error
      } finally {
        console.log(this.answer)
      }
      
    }
  }
}
</script>

<template>
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</template>