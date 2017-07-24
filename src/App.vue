<template>
     <div id="root">
          <router-view></router-view>
     </div>
</template>

<script>
export default {
    data () {
        return {

        }
    }
}
</script>


<style lang="scss">
body{
    overflow-x:hidden
}
*{
    margin: 0;
    padding: 0;
    font-size:16px;
    font-family: 微软雅黑,Arial;
    line-height: 1.2em;
    box-sizing: border-box;
}
img{
    width: 100%;
    height: 100%;
}
a{
    text-decoration: none;
    color: #222;
}
</style>

