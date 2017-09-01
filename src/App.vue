<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addItems"/>
    <ul>
      <li v-for="item in items" v-bind:class="{'finished':item.isFinished}" v-on:click="toggleFinished(item)">
        {{item.label}}
      </li>
    </ul>

  </div>
</template>

<script>
  import Store from './storage'
export default {
  data:function () {
    return {
      title:"this is a vue",
      items:Store.fetch(),
      newItem:'',
    }
  },
  watch:{
    items:{
      handler:function (items) {
        Store.save(items);
      },
      deep:true,
    }

  },

  methods:{
      toggleFinished:function(item){
      item.isFinished=!item.isFinished;
    },
    addItems:function () {
        this.items.push({
          label:this.newItem,
          isFinshed:false
        })
        this.newItem='';


    }
  },
}
</script>

<style>
  .finished{
    text-decoration: underline;
  }
  html{
    height:100%;
  }
  body{
    display:flex;
    align-items: center;
    justify-content: center;
    height:100%;
  }
</style>
