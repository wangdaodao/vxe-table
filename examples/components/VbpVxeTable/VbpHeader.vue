<template>
  <tr v-if="data.length" class="custom-tr">
    <th
      class="vxe-header--column custom-th"
      v-for="(item, index) of list"
      :colspan="item.colspan"
      :key="index"
      :class="[item.visible ? 'is-visible' : 'is-hidden', item.disabled ? 'is-disabled' : '']"
    >
      <div class="vxe-cell" v-html="item.html"></div>
    </th>
  </tr>
</template>
<script>
export default {
  name: 'VbpVxeHeader',
  props: {
    data: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    list () {
      const listNew = this.data.filter(item => !item.hidden)
      listNew.forEach(item => {
        if (typeof item.visible === 'undefined') {
          item.visible = true
        }
        if (typeof item.disabled === 'undefined') {
          item.disabled = false
        }
      })
      return listNew
    }
  }
}
</script>
<style lang="scss" scoped>
.custom-tr {
  .custom-th {
    background-color: #fff7e7;
    padding: 0;
    &.is-hidden {
      display: none;
    }
  }
}
</style>
