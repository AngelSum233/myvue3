<template>
  <div>
    <span>{{treemsg}}{{treeuser.length}}</span>
  </div>
</template>

<script>
import { inject, onMounted, toRefs, reactive } from 'vue'
export default {
  setup () {
    const state = reactive({
      items: ['Feed a cat', 'Buy milk']
    })

    const treeuser = inject('user')
    const treemsg = inject('msg')

    onMounted(() => {
      console.log(`Injected property: ${treeuser.length}`) // > 注入 property: 4
    })

    return {
      ...toRefs(state),
      treeuser,
      treemsg
    }
  }
}
</script>
