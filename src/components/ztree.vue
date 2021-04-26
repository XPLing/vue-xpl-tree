<template>
  <div class="ztree" :id="ztreeId"></div>
</template>

<script>
import * as $ from 'jquery'

if (!window.jQuery) {
  window.jQuery = $
}
require('@ztree/ztree_v3/js/jquery.ztree.all')
require('@ztree/ztree_v3/js/jquery.ztree.exhide')
require('@/assets/ztree/fuzzysearch.module')

export default {
  props: {
    setting: {
      type: Object,
      require: false,
      default: function () {
        return {}
      }
    },
    nodes: {
      type: Array,
      require: true,
      default: function () {
        return []
      }
    }
  },
  data () {
    return {
      ztreeId: 'ztree_' + parseInt(Math.random() * 1e10),
      ztreeObj: null,
      list: [],
      ztreeSetting: {
        view: {
          showIcon: false         // default to hide icon
        },
        callback: {
          beforeAsync: (...arg) => {
            this.$emit('beforeAsync', ...arg)
          },
          beforeCheck: (...arg) => {
            this.$emit('beforeCheck', ...arg)
          },
          beforeClick: (...arg) => {
            this.$emit('beforeClick', ...arg)
          },
          beforeCollapse: (...arg) => {
            this.$emit('beforeCollapse', ...arg)
          },
          beforeDblClick: (...arg) => {
            this.$emit('beforeDblClick', ...arg)
          },
          beforeDrag: (...arg) => {
            this.$emit('beforeDrag', ...arg)
          },
          beforeDragOpen: (...arg) => {
            this.$emit('beforeDragOpen', ...arg)
          },
          beforeDrop: (...arg) => {
            this.$emit('beforeDrop', ...arg)
          },
          beforeEditName: (...arg) => {
            this.$emit('beforeEditName', ...arg)
          },
          beforeExpand: (...arg) => {
            this.$emit('beforeExpand', ...arg)
          },
          beforeMouseDown: (...arg) => {
            this.$emit('beforeMouseDown', ...arg)
          },
          beforeMouseUp: (...arg) => {
            this.$emit('beforeMouseUp', ...arg)
          },
          beforeRemove: (...arg) => {
            this.$emit('beforeRemove', ...arg)
          },
          beforeRename: (...arg) => {
            this.$emit('beforeRename', ...arg)
          },
          beforeRightClick: (...arg) => {
            this.$emit('beforeRightClick', ...arg)
          },
          onAsyncError: (...arg) => {
            this.$emit('onAsyncError', ...arg)
          },
          onAsyncSuccess: (...arg) => {
            this.$emit('onAsyncSuccess', ...arg)
          },
          onCheck: (...arg) => {
            this.$emit('onCheck', ...arg)
          },
          onClick: (...arg) => {
            this.$emit('onClick', ...arg)
          },
          onCollapse: (...arg) => {
            this.$emit('onCollapse', ...arg)
          },
          onDblClick: (...arg) => {
            this.$emit('onDblClick', ...arg)
          },
          onDrag: (...arg) => {
            this.$emit('onDrag', ...arg)
          },
          onDragMove: (...arg) => {
            this.$emit('onDragMove', ...arg)
          },
          onDrop: (...arg) => {
            this.$emit('onDrop', ...arg)
          },
          onExpand: (...arg) => {
            this.$emit('onExpand', ...arg)
          },
          onMouseDown: (...arg) => {
            this.$emit('onMouseDown', ...arg)
          },
          onMouseUp: (...arg) => {
            this.$emit('onMouseUp', ...arg)
          },
          onRemove: (...arg) => {
            this.$emit('onRemove', ...arg)
          },
          onRename: (...arg) => {
            this.$emit('onRename', ...arg)
          },
          onRightClick: (...arg) => {
            this.$emit('onRightClick', ...arg)
          }
        }
      }
    }
  },
  methods: {
    updateTree (isUpdate = true) {
      if (isUpdate) {
        this.init()
      }
    },
    init () {
      this.list = this.nodes
      // update tree
      if (this.ztreeObj) {
        this.ztreeObj.destroy()
      }
      this.$nextTick(() => {
        this.ztreeObj = $.fn.zTree.init($('#' + this.ztreeId), Object.assign({}, this.ztreeSetting, this.setting), this.list)
        this.$emit('onCreated', this.ztreeObj)
      })
    }
  },
  watch: {
    // nodes: {
    //   handler: function (nodes) {
    //     this.list = nodes
    //     // update tree
    //     if (this.ztreeObj) {
    //       this.ztreeObj.destroy()
    //     }
    //     this.$nextTick(() => {
    //       this.ztreeObj = $.fn.zTree.init($('#' + this.ztreeId), Object.assign({}, this.ztreeSetting, this.setting), this.list)
    //       this.$emit('onCreated', this.ztreeObj)
    //     })
    //   },
    //   deep: true,
    //   immediate: true
    // }
  }
}
</script>

<style scoped lang="scss">
/* beauty ztree! */
@import "ztree.scss";
</style>
