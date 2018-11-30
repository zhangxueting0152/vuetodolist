<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addItem">
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}" v-on:click="switchFinished(item)">{{item.label}}</li>
    </ul>
    <ComponentA msgFromFather="i am your father"
                 v-on:childSay="listenToChild"></ComponentA>
    <p>child words is:{{childWords}}</p>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Store from './store'
import ComponentA from './components/componentA.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    ComponentA
  },
  data: function() {
    return {
      title: 'this is a todolist',
      items: Store.fetch(),
      newItem: '',
      childWords: ''
    }
  },
  watch: {
    items: {
      handler: function(val, oldVal) {
        this.items = val;
        Store.save(this.items);
      },
      deep: true
    }
  },
  methods: {
    switchFinished: function(item) {
      item.isFinished = !item.isFinished;
    },
    addItem: function() {
      this.items.push(
        {
          label: this.newItem,
          isFinished: false
        }
        );
      this.newItem = '';
    },
    listenToChild: function (msg) {
      this.childWords = msg;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished {
  text-decoration: line-through;
}
</style>
