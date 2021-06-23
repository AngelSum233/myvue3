<template>
    <div >
        <span >msg：{{msg}}</span>
        <button @click="clickcount">add</button>
        <span>{{count}}</span>
        <div class="myinput">
            <input type="text" :value="title" @input="$emit('update:title',$event.target.value)">
            <input type="text" :value="content" @input="$emit('update:content',$event.target.value)">
            <span>{{title}}</span>
            <span>{{content}}</span>
        </div>
        <div class="myinput">
            <input type="text" :value="word" @input="handleWord" >
            <span>{{word}}</span>
        </div>
        <div>
            <my-tree></my-tree>
        </div>
    </div>
</template>

<script>
import MyTree from '@/components/MyTree.vue'

export default {
  props: {
    msg: String,
    count: Number,
    title: String,
    content: String,
    word: String,
    wordModifiers: {
      default: () => ({})
    }
  },
  components: {
    'my-tree': MyTree
  },
  //   props: ['word', 'wordModifiers'],
  emits: ['update:title', 'update:content', 'update:word'],
  data () {
    return {

    }
  },
  created () {
    console.log(this.wordModifiers)
  },
  methods: {
    clickcount () {
      this.$emit('counter')
    },
    handleWord (e) {
      let value = e.target.value
      if (this.wordModifiers.cap) {
        value = value.charAt(0).toUpperCase() + value.slice(1)
      }
      this.$emit('update:word', value)
    }
  }
}
</script>

<style scoped>
.myinput{
    display: flex;
    flex-direction: column;
}
</style>
