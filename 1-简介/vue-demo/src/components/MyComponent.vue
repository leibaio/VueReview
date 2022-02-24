<script>
  export default {
    data() {
      return {
        count: 0,
        msg: 'leibaio',
        rawHtml: `<span style="color: red">This should be red.</span>`,
        dynamicId: 44,
        isButtonDisabled: true,
        objectOfAttrs: {
          id: 'container',
          class: 'wrapper'
        },
        number: 45,
        ok: 1,
        message: 'petronas',
        seen: true,
        url: 'https://leibaio.space',
      }
    },

    methods: {
      increment() {
        this.count++
      }
    },

    mounted() {
      console.log(`The initial count is ${this.count}.`);
    }
  }
</script>

<template>    
  <button @click="increment">the count is: {{ count }}</button>

  <br>

  <span>Message: {{ msg }}</span>

  <p>Using text interpolation: {{ rawHtml }}</p>

  <p>Using v-html directive: <span v-html="rawHtml"></span></p>

  <div :id="dynamicId">{{ dynamicId }}</div>

  <button :disabled="isButtonDisabled">Button</button>

  <div :="objectOfAttrs">{{ objectOfAttrs.id }}</div>

  <div>{{ number - 1 }}</div>

  <div>{{ ok ? 'YES' : 'NO' }}</div>

  <div>{{ message.split('').reverse().join('') }}</div>

  <p v-if="seen">Now you see me</p>

  <a :href="url"> ... </a>

  <p @click=""> click me </p>
</template>