<template>
  <div class="Todolist">
  <div class="header">
    <h1 class="hader-h1">TodoList</h1>
    <input type="text" v-model="msg" @keyup.enter="addFun()" class="header-input"/>
    <button @click="addFun()" class="header-button">添加</button>
  </div>
  <div class="content" v-show="hasNodata">
    <div class="going">
      <h1 class="going-h1">进行中</h1>
      <ul>
        <li v-for="(item,key) in list" v-if="!item.checked" :key="key" class="going-li">
          <input type="checkbox" v-model="item.checked" @change="saveList()" class="checkbox"/>
          <p class="p">{{item.title}}</p>
          <button @click="moveFun(key)" class="button">移除</button></li>
      </ul>
    </div>
    <div class="going">
      <h1 class="going-h1">已完成</h1>
      <ul>
        <li v-for="(item,key) in list" v-if="item.checked" :key="key" class="haddone-li" >
          <input type="checkbox" v-model="item.checked"  class="checkbox"/>
          <p class="p">{{item.title}}</p>
          <button @click="moveFun(key)" class="haddone-button">移除</button></li>
      </ul>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Todolist',
  data () {
    return {
      msg: '',
      list: []
    }
  },
  methods: {
    addFun () {
      this.list.push({
        title: this.msg
      })
      this.msg = ''
      localStorage.setItem('list', JSON.stringify(this.list))
    },
    moveFun (key) {
      confirm('是否移除' + this.list[key].title + '?')
      this.list.splice(key, 1)
      localStorage.setItem('list', JSON.stringify(this.list))
    },
    saveList () {
      localStorage.setItem('list', JSON.stringify(this.list))
    }
  },
  mounted () {
    var list = JSON.parse(localStorage.getItem('list'))
    if (list) {
      this.list = list
    }
  },
  computed: {
    hasNodata () {
      return this.list.length
    }
  }
}
</script>

<style scoped>
  .header{
    width: 100%;
    text-align: center;
    background:black;
    height: 50px;
    line-height: 50px;
  }
  .hader-h1{
    display: inline-block;
    font-size: 20px;
    font-weight: bolder;
    color: white;
  }
  .header-input{
    display: inline-block;
    width: 400px;
    height:25px;
    border-radius: 5px;
    margin-left: 50px;
    margin-top: -5px;
  }
  .header-button{
    margin-top: -5px;
    border-radius: 2px;
    margin-left: 10px;
  }
  .content{
    width: 100%;
    height: 100%;
  }
  .going{
    margin-left: 250px;
    margin-top: 20px;
  }
  .going-h1{
    font-size: 20px;
    font-weight: bolder;
    color: #000;
  }
  .going-li{
    height: 30px;
    line-height: 30px;
    width: 500px;
    background: white;
    margin-top: 10px;
    border-left: 8px solid darkslategrey;
    border-radius: 3px;
  }
  .checkbox{
    margin-left: 20px;
  }
  .p{
    display: inline-block;
    margin-left: 180px;
  }
  .button{
    float: right;
    margin-right: 20px;
    margin-top: 5px;
    background: #25a4bb;
    border-radius: 5px;
    color: white;
    font-size: 10px;
    font-weight: bold;
    padding: 2px;
  }
  .haddone-li{
    height: 30px;
    line-height: 30px;
    width: 500px;
    background: gainsboro;
    margin-top: 10px;
    border-left: 8px solid darkolivegreen;
    border-radius: 3px;
  }
  .haddone-button{
    float: right;
    margin-right: 20px;
    margin-top: 5px;
    background: gray;
    border-radius: 5px;
    color: white;
    font-size: 10px;
    font-weight: bold;
    padding: 2px;
  }
</style>
