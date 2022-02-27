<script>
export default {
  // 传递props：如果在构建一个博客，可能需要一个博客文章的组件。若所有的文章分享相同的视觉布局，但有不同的内容。要实现这样的效果自然要向组件中传递数据。例如每篇文章的标题和内容。
  props: ['title'],
  // 当一个值被传递给 prop 时，一个组件可以有任意多的  props，默认情况下，任何值都可以传递给任何 prop。当一个 prop 被注册后，可以向这样自定义 attribute 的形式传递数据
  posts: [
      { id: 1, title: 'My journey with Vue' },
      { id: 2, title: 'Blogging with Vue' },
      { id: 3, title: 'Why Vue is so fun' }
  ],
  postFontSize: 1
}
</script>

<template>
      <h4>{{ title }}</h4>      
      <button @click="$emit('enlarge-text')">放大文字</button>
</template>