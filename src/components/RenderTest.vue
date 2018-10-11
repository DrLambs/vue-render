<template>
  <div class="render">
    <h1>{{ msg }}</h1>
    <renderComponent></renderComponent>
    <renderComponentList></renderComponentList>
  </div>
</template>

<script>
export default {
  name: 'RenderTest',
  props: {
    msg: String,
    level: {
      type: Number,
      required: true
    },
    items: {
      type: Array,
      required: false
    }
  },
  components: {
    renderComponent: {
      /**
       * render: 渲染函数
       * 参数: createElement
       * 参数类型: Function
       */
      render: function (createElement) {
        let _this = this['$options'].parent
        console.log(_this)
        console.log(_this.$slots)
        let _header = _this.$slots.header
        /**
         * createElement 本身也是一个函数，它有三个参数
         * 
         * 返回值: VNode
         * 
         * 1. 一个 HTML 标签字符串，组件选项对象，或者解析上述任何一种的一个 async 异步函数。必需参数。{String | Object | Function} - 就是你要渲染的最外层标签
         * 
         * 2. 一个包含模板相关属性的数据对象你可以在 template 中使用这些特性。可选参数。{Object} - 1中的标签的属性
         * 
         * 3. 子虚拟节点 (VNodes)，由 `createElement()` 构建而成，也可以使用字符串来生成“文本虚拟节点”。可选参数。{String | Array} - 1的子节点，可以用 createElement() 创建，文本节点直接写就可以
         */
        return createElement(                 
          'h' + _this.level,   // 标签名称 - 第一个参数
          {
            style: {
              color: 'gray',
              border: '1px solid pink'
            }
          },   // 第二个单数
          [
            _this.$slots.default, 
            'child', 
            createElement(
              'div',
              {
                'class': {
                  'slotsWrap': true
                }
              },
              [createElement('div', _header)]
            )
          ] // 子元素数组 - 第三个参数
        )
      }
    },
    renderComponentList: {
      render: function (createElement) {
        let _this = this['$options'].parent

        if (_this.items.length) {
          return createElement(
            'ul', 
            _this.items.map(function (item) {
              return createElement('li', item.name)
            })
          )
        } 
        else {
          return createElement('p', 'No items found.')
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

