<template>
  <vxe-colgroup v-bind="$attrs" :title="label || $attrs.title" v-if="children.length && _visible">
    <vbp-vxe-column v-for="(item, index) of children" v-bind="item" :key="index"></vbp-vxe-column>
  </vxe-colgroup>
  <vxe-column
    v-bind="$attrs"
    :title="label || $attrs.title"
    :fixed="_fixed"
    :field="prop || $attrs.field"
    :visible="_visible"
    v-else
  >
    <template #checkbox="{ row, checked, indeterminate }" v-if="$attrs.type === 'checkbox'">
      <span class="custom-checkbox" @click.stop="checkboxChange(row, checked, indeterminate)" :title="$attrs.tooltips">
        <i v-if="indeterminate" class="vxe-icon-square-minus-fill"></i>
        <i v-else-if="checked" class="vxe-icon-square-checked-fill"></i>
        <i v-else class="vxe-icon-checkbox-unchecked"></i>
      </span>
    </template>
  </vxe-column>
</template>
<script>
export default {
  name: 'VbpVxeColumn',
  inheritAttrs: false,
  props: {
    children: {
      type: Array,
      default: () => []
    },
    label: [String, Number],
    prop: [String, Number],
    fixed: [String, Boolean]
  },
  computed: {
    compTooltip () {
      return function ($attrs, row) {
        const content = $attrs.tooltipRender(row)

        return content
      }
    },
    // eslint-disable-next-line vue/return-in-computed-property
    _fixed () {
      if (typeof this.fixed === 'string') {
        return this.fixed
      }
      if (typeof this.fixed === 'boolean' && this.fixed) {
        return 'left'
      }
    },
    _visible () {
      if (Object.hasOwn(this.$attrs, 'hidden')) {
        return !this.$attrs.hidden
      }
      return Object.hasOwn(this.$attrs, 'visible') ? this.$attrs.visible : true
    }
  },
  methods: {
    checkboxChange (row, checked) {
      this.$parent.toggleCheckboxRow(row)
      const records = this.$parent.getCheckboxRecords()
      this.$parent.$emit('checkbox-change', records, row, !checked)
    }
  }
}
</script>
