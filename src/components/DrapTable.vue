<script>
export default {
  name: "DrapTable",
  data() {
    return {
      beginIdx: null,
      sourceIdx: null,
      components: {
        body: {
          wrapper: {
            render: function (createElement) {
              return createElement(
                "transition-group",
                {
                  props: {
                    tag: "tbody",
                    name: "slide",
                  },
                },
                this.$slots.default
              );
            },
          },
        },
      },
      expandedRow: [],
    };
  },
  props: {
    dataSource: {
      type: Array,
    },
  },
  mounted() {
    this.expandedRow = [];
  },
  methods: {
    swapArray(arr, idx1, idx2) {
      arr[idx1] = arr.splice(idx2, 1, arr[idx1])[0];
    },
    customRow(_, index) {
      return {
        attrs: {
          draggable: true,
        },
        style: {
          cursor: "pointer",
        },
        class: {
          "clear-bg": this.beginIdx === index,
          "source-el": this.sourceIdx === index,
        },
        on: {
          dragstart: (event) => {
            let ev = event || window.event;
            ev.stopPropagation();
            // 得到源目标数据
            this.beginIdx = index;
            this.sourceIdx = index;
          },
          // 拖动元素经过的元素
          dragover: (event) => {
            let ev = event || window.event;
            ev.preventDefault();
          },
          dragenter: (event) => {
            let ev = event || window.event;
            ev.preventDefault();
            if (this.sourceIdx !== index) {
              this.swapArray(this.dataSource, this.sourceIdx, index);
              this.sourceIdx = index;
            }
          },
          dragend: (event) => {
            let ev = event || window.event;
            ev.preventDefault();
            this.sourceIdx = null;
            this.beginIdx = null;
          },
        },
      };
    },
    expandedRowsChange(expandedRow) {
      this.expandedRow = expandedRow;
    },
  },
  render(createElement) {
    return createElement("a-table", {
      attrs: {
        ...this.$attrs,
        dataSource: this.$props.dataSource,
        customRow: this.customRow,
        components: this.components,
        defaultExpandAllRows: true,
        expandedRowKeys: this.expandedRow,
      },
      on: {
        ...this.$listeners,
        expandedRowsChange: this.expandedRowsChange
      },
      scopedSlots: this.$scopedSlots,
    });
  },
};
</script>
<style>
.source-el {
  transform: translate3d(0, 0, 2px);
}

.clear-bg > td {
  background-color: #fff !important;
}

.source-el > td {
  background-color: #e6f7ff !important;
}

.slide-move {
  transition: transform 0.3s linear;
}
</style>