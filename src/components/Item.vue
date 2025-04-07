<template>
  <li>
    <span v-if="typeof element === 'string'">{{ element }} (+)</span>
    <ul v-else-if="Array.isArray(element)">
      <Item
        v-for="x in element"
        :key="x.id"
        :element="x"
      />
    </ul>
    <template v-else>
      <span>{{ element.label }}</span>
      <span v-if="element.menu && element.menu.length > 0">(+)</span>
      <ul v-if="element.menu && element.menu.length > 0">
        <Item
          v-for="x in element.menu"
          :key="x.id || Math.random()"
          :element="x"
        />
      </ul>
    </template>
  </li>
</template>

<script>
/* eslint-disable vue/multi-word-component-names */

import { defineComponent } from 'vue'
// import Item from '@/components/Item.vue'
export default defineComponent({
  name: 'Item',
  props: {
    element: {
      type: [String, Array, Object],
      default: () => ([])
    },
    menus: {
      type: [Array],
      default: () => ([])
    }
  },
  data: function () {
    return {
    }
  }
})
</script>
