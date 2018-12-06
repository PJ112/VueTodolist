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
    background:black;
    height:80px;
    line-height: 80px;
  }
  .hader-h1{
    display: inline-block;
    font-size: 40px;
    font-weight: bolder;
    color: white;
    margin-left: 20%;
  }
  .header-input{
    display: inline-block;
    width: 50%;
    height:50px;
    border-radius: 5px;
    margin-left: 5%;
    margin-top: -10px;
  }
  .header-button{
    float: right;
    height:50px;
    margin-top: -5px;
    margin-top: 25px;
    border-radius: 5px;
    width: 50px;
    height: 40px;
    margin-right: 11%;
  }
  .content{
    width: 100%;
    height: 100%;
  }
  .going{
    margin-left: 20%;
    margin-top: 5%;
  }
  .going-h1{
    font-size: 30px;
    font-weight: bolder;
    color: #000;
  }
  .going-li{
    height: 60px;
    line-height: 60px;
    width: 70%;
    background: white;
    margin-top: 2%;
    border-left: 8px solid darkseagreen;
    border-radius: 8px;
    font-size: 20px;
    font-weight: bold;
  }
  .checkbox{
    margin-left: 2%;
  }
  .p{
    display: inline-block;
    margin-left: 40%;
  }
  .button{
    float: right;
    margin-right: 5%;
    background: #25a4bb;
    border-radius: 5px;
    color: white;
    font-size: 10px;
    font-weight: bold;
    padding: 5px;
    margin-top: 10px;
  }
  .haddone-li{
    height: 60px;
    line-height: 60px;
    width: 70%;
    background: white;
    margin-top: 2%;
    border-left: 8px solid darkslategrey;
    border-radius: 8px;
    font-size: 20px;
    font-weight: bold;
  }
  .haddone-button{
    float: right;
    margin-right: 5%;
    background: #25a4bb;
    border-radius: 5px;
    color: white;
    font-size: 10px;
    font-weight: bold;
    padding: 5px;
    margin-top: 10px;
  }
</style>
