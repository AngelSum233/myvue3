<template>
  <div>
    <ul>
      <li v-for="( item, index ) in items" :key="index">
        <slot :item="item" :index="index"></slot>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data () {
    return {
      items: ['Feed a cat', 'Buy milk']
    }
  }
}
</script>
