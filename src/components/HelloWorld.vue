<template>
  <div class="hello">
    <tree-menu :model="treeData"></tree-menu>
  </div>
</template>

<script>
import treeMenu from '../publice/treeMenu'
export default {
  name: 'HelloWorld',
  components:{treeMenu},
  data () {
    return {
        treeData:{
            name: 'My Tree',
            children: [
                { name: 'hello' },
                { name: 'watdfs' },
                {
                name: 'child folder',
                children: [
                    {
                    name: 'child folder',
                    children: [
                        { name: 'hello' },
                        { name: 'wat' }
                    ]
                    },
                    { name: 'hello' },
                    { name: 'wat' },
                    {
                    name: 'child folder',
                    children: [
                        { name: 'hello' },
                        { name: 'wat' }
                    ]
                    }
                ]
                }
            ]
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .hello{
        width: 250px;
        margin:  0 auto;
        border:  1px solid #ccc;
    }
</style>
