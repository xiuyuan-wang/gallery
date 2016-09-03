<template>
  <div id="app">
  <h1 v-html="title"></h1>
  <input v-model="newItem" v-on:keyup.enter="addNew"></input>
  <ul>
  <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="finishesFor(item)">

    {{item.label}}
  </li>
  </ul>

  <p>child tells ne:{{childWords}}</p>
  <hello hehehe="wangxiuyuan---"  ></hello>
  </div>
</template>

<script>


import Store from './store'
console.log(Store)
import Hello from './components/Hello'

export default{


  data: function(){
    return {
    title: '<span>hehe</span>this is a todo list',
    items:Store.fetch(),
    childWords:''
   

    }
  },
  components: { Hello },
  watch: {
    items: {
      handler: function(items){
        Store.save(items)      

      },
      deep: true

    }

  },
  events:{
  'child-tell-me-something':function(smg){
   this.childWords=smg;


  }


  },

   methods:{

     finishesFor: function (item) {
     console.log(item.isFinished=!item.isFinished);
    },

     addNew: function(){

     this.items.push({
      label: this.newItem,
      isFinished: false

     })
     this.newItem=''

     }
    
    }
    
}

</script>

<style>
html {
  height: 100%;
}
.finished{
color: red;

}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

#app {
  color: #2c3e50;
  margin-top: -100px;
  max-width: 600px;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}
</style>
