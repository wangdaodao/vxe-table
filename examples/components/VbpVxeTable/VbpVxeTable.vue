<template>
  <vxe-table ref="xTable" v-bind="{ ...defaultConfig, ...$attrs }" v-on="$listeners" @resizable-change="resizableChange" class="vxe-table-wrap">
    <template #header-append v-if="theadList.length">
      <VbpHeader :data="theadList"></VbpHeader>
    </template>
    <template slot="empty">
      <slot name="empty">
        <div>123</div>
      </slot>
    </template>
    <template v-for="(item, index) in columnList">
      <slot v-if="item.slot" :name="item.slot"></slot>
      <VbpColumn v-else :key="index" v-bind="item"></VbpColumn>
    </template>
  </vxe-table>
</template>
<script>
import VbpColumn from './VbpColumn.vue'
import VbpHeader from './VbpHeader.vue'
export default {
  name: 'VbpTable',
  components: { VbpColumn, VbpHeader },
  inheritAttrs: false,
  props: {
    theadList: {
      type: Array,
      default: () => []
    },
    columnList: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      defaultConfig: {
        'show-header-overflow': true,
        border: true,
        size: 'mini',
        'tree-config': {
          transform: true,
          parentField: 'pid',
          iconOpen: 'el-icon-arrow-down',
          iconClose: 'el-icon-arrow-right',
          expandAll: true,
          reserve: true,
          indent: 13
        },
        'scroll-y': { enabled: true, gt: 0, oSize: 5 },
        'scroll-x': { enabled: true, gt: 0, oSize: 5 },
        'column-config': { useKey: true, resizable: true },
        'row-config': { useKey: true, isHover: true },
        'checkbox-config': { showHeader: false }
      }
    }
  },
  methods: {
    resizableChange () {
      const $table = this.$refs.xTable
      $table.refreshScroll(true)
    }
  }
}
</script>
