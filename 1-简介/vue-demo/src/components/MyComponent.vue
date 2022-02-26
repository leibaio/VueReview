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
        },
        numbers: [1, 2, 3, 4, 5],
        sets: [[1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]],
        name: 'Vue.js',
        inputMsg: '',
        checkedNames: [],
      }
    },

    methods: {
      increment() {
        this.count++
      },
      doSomething() {
        alert("123")
      },
      even(numbers) {
        return this.numbers.filter(n => n % 2 === 0)   
      },
      greet(event) {
        // 方法中的`this`指向当前活跃的组件
        alert(`Hello ${this.name}!`)
        // `event` 是原生DOM事件
        if (event) {
          alert(event.target.tagName)
        }
      },
      say(message) {
        alert(message)
      },
    },

    mounted() {
      // `this`指向当前组件实例
      console.log(`组件现在已被挂载`);
      this.count = 2;     
      console.log(`The initial count is ${this.count}.`);
    },

    computed: {
      // 计算和方法在结果上相同，但是计算属性值会基于其响应式依赖被缓存
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
      },
      evenNumbers() {
        return this.numbers.filter(n => n % 2 === 0)
      },
    }
  }
</script>

<template>    
  <!-- 侦听器 -->
  <!-- 在选项式 API 中，我们可以使用 watch 在每次响应式 property 发送变化时出发一个函数 -->

  <!-- 生命周期钩子 -->
  <!-- 注册周期钩子：mounted 钩子可以用来组件完成初始渲染并创建DOM节点后运行代码 -->
  <!-- 还有一些其他钩子，会在实例生命周期的不同阶段被调用，最常用的 mounted, updated, unmounted ，所有生命周期钩子函数的 this 上下文都会自动指向当前调用它的组件。注意：避免使用箭头函数定义生命周期的钩子，因为这样无法在函数中通过 this 获取组件实例 -->

  <!-- 表单输入绑定 -->
  <input :value="text" @input="event => text = event.target.value">
  <!-- 在处理表单时，手动连接值绑定和更改事件监听器可能会麻烦，v-model 简化了这一步骤 -->
  <input v-model="text">

  <!-- 基本用法：文本 -->
  <p>输入的信息: {{ inputMsg }}</p>
  <input v-model="inputMsg" placeholder="edit me">

  <!-- 多行文本 -->
  <span>多行信息: {{ inputMsg }}</span>
  <p style="white-space: pre-line;"> {{ inputMsg }}</p>
  <textarea v-model="inputMsg" placeholder="add multiple lines"></textarea>

  <!-- 复选框 -->
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">{{ checked }}</label>

  <!-- 可以将多个复选框绑定到同一个数组或者集合 -->
  <div>选择的名字有: {{ checkedNames }}</div>

  <input type="checkbox" id="jack" value="jack" v-model="checkedNames">
  <label for="jack">jack</label>

  <input type="checkbox" id="tom" value="tom" v-model="checkedNames">
  <label for="tom">tom</label>

  <input type="checkbox" id="mike" value="mike" v-model="checkedNames">
  <label for="mike">mike</label>

  <!-- 修饰符 -->
  <!-- 默认情况下，v-model 会在每次input后更新数据（IME composition阶段的状态除外）。可以添加 lazy 修饰符来改为每次 change 事件后更新数据： -->
  <input type="text" v-model.lazy="msg">

  <!-- 如果想让用户输入自动转换为数字，可以在v-model后添加 .number 来管理输入 -->
  <input type="text" v-model.number="age" />

  <!-- 如果要默认自动去除用户输入内容中两端的空格，可以在v-model后添加 .tirm -->
  <input type="text" v-model.trim="msg">

  <!-- 内联事件处理器常用于简单场景，如 -->
  <button @click="increment">the count is: {{ count }}</button>

  <!-- 当事件处理器逻辑变得复杂，v-on也接受方法名或者某个方法的访问 -->
  <button @click="greet">Greet</button>

  <!-- 在内联处理器调用方法 -->
  <button @click="say('hello')">say hello</button>
  <button @click="say('bye')">say bye</button>

  <!-- 在内联事件处理器中访问事件参数 -->
  <!-- 事件修饰符 -->
  <!-- 按键修饰符 -->


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

  <!-- 数组变化侦测 -->
  <!-- 诱变方法：push() pop() shift()删除第一个元素 unshift()在最前面插入一个或多个元素 splice()从数组中删除指定的一个或多个元素  sort() reverse() -->
  <!-- 诱变方法，顾名思义，会对调用他们的方法进行更改。相对的，非诱变方法，如filter(), concat(), slice()从数组中提取指定的一个或多个元素，都不会更改原数组，总是返回一个新数组 -->

  <!-- 展示过滤或排序后的结果 -->
  <ul>
    <li v-for="n in evenNumbers">{{ n }}</li>
  </ul>

  <!-- 当计算属性不可行时（比如在多层嵌套的v-for循环中），可以使用methods --> 
  <ul v-for="numbers in sets">
    <li v-for="n in even(numbers)">{{ n }}</li>
  </ul>

  <!-- 对于reverse() 和 sort() 保持谨慎，会改变原始数组，计算函数中不应该这么做。调用之前创建数组 -->
</template>

<style scoped>

</style>