<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family:'Microsoft YaHei', 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 14px;
  /* position: relative; */
}
*{
  box-sizing: border-box;
}
html,body{
  padding:0;
  margin:0;
  height:100%;
}
.wrapper{
  width:1200px;
  margin: 0 auto;
}
p,ul,li{
  padding:0;
  margin:0;
  list-style: none;
}
.lf{
  float: left;
}
.rt{
  float: right;
}
@media screen and (max-width: 768px){
  #app {
    font-size:12px!important;
  }
  .wrapper{
    width:100%;
  }
}
</style>
