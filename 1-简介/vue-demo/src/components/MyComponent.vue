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
        author: {
          name: 'John Doe',
          books: [
            'Vue 2 - Advanced Guide',
            'Vue 3 - Basic Guide',
            'Vue 4 - The Mystery'
          ]
        },
        firstName: 'John',
        lastName: 'Doe',
        isActive: true,
        hasError: false,
        awesome: true,
      }
    },

    methods: {
      increment() {
        this.count++
      },
      doSomething() {
        alert("123")
      }
    },

    mounted() {
      // `this`指向当前组件实例
      this.count = 2;     
      console.log(`The initial count is ${this.count}.`);
    },

    computed: {
      // 一个计算属性的 getter
      publishedBooksMessage() {
        // `this` 指向当前组件实例
        return this.author.books.length > 0 ? 'Yes' : 'No'
      },
      now() {
        return Date.now()
      },
      fullName: {
        // getter
        get() {
          return this.firstName + ' ' + this.lastName
        },
        // setter
        set(newValue) {
          //使用解构赋值
          [this.firstName, this.lastName] = newValue.split(' ')
        }
      }
    }
  }
</script>

<template>    
  <button @click="increment">the count is: {{ count }}</button>

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

  <button @click="doSomething"> click me </button>

  <button @click="increment">{{ count }}</button>

  <p>Has published books:</p>
  <span>{{ publishedBooksMessage }}</span>

  <p>{{ now }}</p>

  <span>{{ this.fullName }}</span>

  <div class="static" :class="{ active: isActive, 'text-danger': hasError }">class</div>

  <button @click="awesome = !awesome">切换</button>

  <h1 v-if="awesome">Vue最棒啦</h1>
  <h1 v-else>这是else</h1>

  <h1 v-show="awesome">HELLO</h1>
  <!-- v-show会在DOM渲染中保留该节点，仅仅切换了该元素的display的CSS属性 -->

  <!-- v-if VS v-show -->
  <!-- v-if是真是的按条件渲染，是懒加载的，如果初次渲染为false，不会做任何事，条件区域在条件首次变为true才渲染 ；
  相比之下，v-show简单许多，无论如何，始终会被渲染，仅做CSS类的切换； 因此，需要频繁切换时，用v-show更好，而不太会改变，用v-if更合适-->
</template>