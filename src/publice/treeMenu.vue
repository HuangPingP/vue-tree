<template>
  <ul class="item">
    <li >
      <div 
      :class="{bold: isFolder,'item-info':true}" 
      @click="toggle" >
        <!-- 伸缩图标 -->
        <span 
        v-if="isFolder" 
        :class="{'iconfont':true,'icon-right-allow':!open,'icon-down-allow':open}">
        </span>
        <span class="item-name ellipsis">{{ model.name }}</span>

        <!-- 操作栏 -->
        <p class="edit-box">
          <i class="iconfont icon-add" @click="addChild"></i>
          <i class="iconfont icon-edit"></i>
          <i class="iconfont icon-dele"></i>
        </p>
      </div>

      <!-- 组件递归调用 -->
      <ul class="item-child" v-show="open" v-if="isFolder">
        <item 
          v-for="(model, index) in model.children" 
          :key="index" 
          :model="model">
        </item>
      </ul>
    </li>
  </ul>
</template>

<script>
/**
 * name 必须定义，否则无效
 */
  import Vue from 'vue'
  export default {
    props: ['model'],
    name: 'item',  // 必须给组件命名
    data() {
      return {
         open: true
      }
    },
    computed: {
    isFolder() {
      return this.model.children &&
        this.model.children.length
    }
  },
  methods: {
    toggle() {
      if (this.isFolder) {
        this.open = !this.open
      }
    },
    addChild() {
      if (!this.isFolder) {
        Vue.set(this.model, 'children', [])
        this.open = true
      }
      this.model.children.push({
        name: 'new stuff'
      })
    }
  }
}
</script>
<style lang='less' scoped>
.item {
  font-size: 14px;
  cursor: pointer;
  margin: 5px;
  text-align: left;
}
.bold {
  font-weight: bold;
}
ul {
  line-height: 28px;
}
.item-info{
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.item-child{
  padding-left:14px; 
}

.item-name{
  flex: 1;
}
.edit-box{
  visibility: hidden;
  margin-left: 6px;
  z-index: 80;
  i{
    padding: 0 4px;
  }
}
.item-info:hover .edit-box{
   visibility: visible
}
</style>
