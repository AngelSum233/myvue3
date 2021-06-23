<template>
  <div class="home">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <my-com :msg="msg" :count="count" @counter="counter"
     v-model:title="bookTitle" v-model:content="content"
     v-model:word.cap="word" />
     <span>provide的测试{{bookTitle}}</span>
     <my-list>
       <template v-slot:default="slotProps">
        <i class="fas fa-check"></i>
        <span class="green">{{ slotProps.item }}</span>
      </template>
     </my-list>
  </div>
</template>

<script>
// @ is an alias to /src
import myCom from '@/components/MyCom.vue'
import myList from '@/components/MyList.vue'
// 获取列表的所有数据
import { toRefs, provide, reactive, ref } from 'vue'
export default {
  name: 'Home',
  components: {
    myCom,
    myList
  },
  setup () {
    const state = reactive({
      msg: '消息',
      count: 1,
      bookTitle: '书名',
      content: '内容',
      word: '',
      dada: [1, 2, 3, 4]
    })
    const msgvalue = state.bookTitle
    const user = reactive(state.dada)
    const msg = ref(msgvalue)

    provide('user', user)
    provide('msg', msg)

    const counter = () => {
      console.log('父组件被点击')
      return state.count++
    }

    return {
      ...toRefs(state),
      counter,
      user,
      msg
    }
  }
  // provide () {
  //   return {
  //     user: this.dada,
  //     msg: Vue.computed(() => this.bookTitle)
  //   }
  // },
  // computed: {
  //   bookTitlevalue () {
  //     return this.bookTitle.length > 3 ? 'aaa' : 'bbb'
  //   }
  // },
  // data () {
  //   return {
  //     msg: '消息',
  //     count: 1,
  //     bookTitle: '书名',
  //     content: '内容',
  //     word: '',
  //     dada: [1, 2, 3, 4]
  //   }
  // },
  // methods: {
  //   counter () {
  //     console.log('父组件被点击')
  //     return this.count++
  //   }
  // }
}
</script>

<style scoped>
.green{
  color: blue;
}
</style>
