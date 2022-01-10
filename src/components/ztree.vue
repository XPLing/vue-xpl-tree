<template>
  <div class="ztree" :id="ztreeId"></div>
</template>

<script>
import * as $ from 'jquery'

if (!window.jQuery) {
  window.jQuery = $
}
require('@/assets/ztree/jquery.ztree.all')
require('@/assets/ztree/jquery.ztree.exhide')
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
            return this.$listeners.beforeAsync && this.$listeners.beforeAsync(...arg)
          },
          beforeCheck: (...arg) => {
            return this.$listeners.beforeCheck && this.$listeners.beforeCheck(...arg)
          },
          beforeClick: (...arg) => {
            return this.$listeners.beforeClick && this.$listeners.beforeClick(...arg)
          },
          beforeCollapse: (...arg) => {
            return this.$listeners.beforeCollapse && this.$listeners.beforeCollapse(...arg)
          },
          beforeDblClick: (...arg) => {
            return this.$listeners.beforeDblClick && this.$listeners.beforeDblClick(...arg)
          },
          beforeDrag: (...arg) => {
            return this.$listeners.beforeDrag && this.$listeners.beforeDrag(...arg)
          },
          beforeDragOpen: (...arg) => {
            return this.$listeners.beforeDragOpen && this.$listeners.beforeDragOpen(...arg)
          },
          beforeDrop: (...arg) => {
            return this.$listeners.beforeDrop && this.$listeners.beforeDrop(...arg)
          },
          beforeEditName: (...arg) => {
            return this.$listeners.beforeEditName && this.$listeners.beforeEditName(...arg)
          },
          beforeExpand: (...arg) => {
            return this.$listeners.beforeExpand && this.$listeners.beforeExpand(...arg)
          },
          beforeMouseDown: (...arg) => {
            return this.$listeners.beforeMouseDown && this.$listeners.beforeMouseDown(...arg)
          },
          beforeMouseUp: (...arg) => {
            return this.$listeners.beforeMouseUp && this.$listeners.beforeMouseUp(...arg)
          },
          beforeRemove: (...arg) => {
            return this.$listeners.beforeRemove && this.$listeners.beforeRemove(...arg)
          },
          beforeRename: (...arg) => {
            return this.$listeners.beforeRename && this.$listeners.beforeRename(...arg)
          },
          beforeRightClick: (...arg) => {
            return this.$listeners.beforeRightClick && this.$listeners.beforeRightClick(...arg)
          },
          onAsyncError: (...arg) => {
            return this.$listeners.onAsyncError && this.$listeners.onAsyncError(...arg)
          },
          onAsyncSuccess: (...arg) => {
            return this.$listeners.onAsyncSuccess && this.$listeners.onAsyncSuccess(...arg)
          },
          onCheck: (...arg) => {
            return this.$listeners.onCheck && this.$listeners.onCheck(...arg)
          },
          onClick: (...arg) => {
            return this.$listeners.onClick && this.$listeners.onClick(...arg)
          },
          onCollapse: (...arg) => {
            return this.$listeners.onCollapse && this.$listeners.onCollapse(...arg)
          },
          onDblClick: (...arg) => {
            return this.$listeners.onDblClick && this.$listeners.onDblClick(...arg)
          },
          onDrag: (...arg) => {
            return this.$listeners.onDrag && this.$listeners.onDrag(...arg)
          },
          onDragMove: (...arg) => {
            return this.$listeners.onDragMove && this.$listeners.onDragMove(...arg)
          },
          onDrop: (...arg) => {
            return this.$listeners.onDrop && this.$listeners.onDrop(...arg)
          },
          onExpand: (...arg) => {
            return this.$listeners.onExpand && this.$listeners.onExpand(...arg)
          },
          onMouseDown: (...arg) => {
            return this.$listeners.onMouseDown && this.$listeners.onMouseDown(...arg)
          },
          onMouseUp: (...arg) => {
            return this.$listeners.onMouseUp && this.$listeners.onMouseUp(...arg)
          },
          onRemove: (...arg) => {
            return this.$listeners.onRemove && this.$listeners.onRemove(...arg)
          },
          onRename: (...arg) => {
            return this.$listeners.onRename && this.$listeners.onRename(...arg)
          },
          onRightClick: (...arg) => {
            return this.$listeners.onRightClick && this.$listeners.onRightClick(...arg)
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
@import "ztree-card";
</style>
