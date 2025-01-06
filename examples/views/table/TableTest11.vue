<template>
  <div>
    <VbpVxeTable
      ref="xTable"
      height="600px"
      size="mini"
      auto-resize
      :sync-resize="true"
      :scroll-y="{ enabled: true, gt: 0, oSize: 5 }"
      show-overflow
      :row-config="{
        useKey: true,
        isHover: true,
        isCurrent: true,
        keyField: 'id',
      }"
      :tree-config="{
        transform: true,
        parentField: 'pid',
        expandAll: true,
        reserve: true,
      }"
      :data="tableData"
      :columnList="tableColumn"
      :theadList="theadList"
    >
      <vxe-column slot="demo2" type="checkbox" field="age" title="age" width="50">
         <template #checkbox="{ row, checked, indeterminate }">
          <span class="custom-checkbox" @click.stop="toggleCheckboxEvent(row)" title="哈哈哈">
            <i v-if="indeterminate" class="vxe-icon-square-minus-fill"></i>
            <i v-else-if="checked" class="vxe-icon-square-checked-fill"></i>
            <i v-else class="vxe-icon-checkbox-unchecked"></i>
          </span>
        </template>
      </vxe-column>
    </VbpVxeTable>
  </div>
</template>

<script>
import VbpVxeTable from '../../components/VbpVxeTable/VbpVxeTable.vue'
import tableData from './data.json'
export default {
  components: { VbpVxeTable },
  data () {
    return {
      tableData,
      theadList: [
        {
          html: '<div>123</div>',
          colspan: 3
        }
      ],
      tableColumn: [
        { slot: 'demo2', title: '选择' },
        { type: 'seq', width: 200, treeNode: true },
        { field: 'name', title: '名称' }
      ]
    }
  },
  methods: {
    toggleCheckboxEvent (row) {
      const $table = this.$refs.xTable.$refs.xTable
      if ($table) {
        $table.toggleCheckboxRow(row)
      }
    }
  }
}
</script>
