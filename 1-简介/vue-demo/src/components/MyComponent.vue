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
        items: [{ message: 'Foo' }, { message: 'Bar'}],
        parentMessage: 'Parent',
        myObject: {
          title: '如何在Vue中渲染列表',
          author: '王小明',
          publishedAt: '2022-02-22'
        }
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

  <!-- 可以使用v-for基于一个数组渲染一个列表。需要一种特殊的语法形式 item in items, items是源数据的数组，而item是对迭代项的别名 -->

  <li v-for="item in items">
    {{ item.message }}
  </li>

  <!-- v-for 块中可以完整地访问父作用域内的属性。v-for也支持使用可选的第二个参数，表示当前项的位置索引 -->

  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>

  <!-- 也可以使用 v-for 来遍历一个对象的所有属性 -->
  <ul>
    <li v-for="value in myObject">
      {{ value }}
    </li>
  </ul>

  <!-- 可以提供第二个参数表示属性名(例如 key) -->
  <ul>
    <li v-for="(value, key) in myObject">
      {{ key }} - {{ value }}
    </li>
  </ul>

  <!-- 可以直接给 v-for 传一个整数值 -->
  <span v-for="n in 10"> {{ n }} </span>
  <!-- 注意此处的n从1而并非0 -->

  <!-- template上的v-for -->
  <ul>
    <template v-for="item in items">
      <li>{{ item.message }}</li>   
    </template>
  </ul>

  <!-- 当Vue更新一个v-for渲染的列表，默认采用“原地修补”的策略。如果数据项顺序发生了改变，Vue不是通过移动DOM元素来匹配条目的顺序，而是在恰当的位置对每个元素进行修补。
  
  为了给Vue一个提示，以便它可以跟踪每个节点的标识，从而重用和重新排序现有的元素，需要为每个项目提供一个唯一的key属性
   -->
  <div v-for="item in items" :key="item.id">
    <li>{{ item.message }}</li>
  </div>
</template>