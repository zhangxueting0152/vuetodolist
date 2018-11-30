<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{msgFromFather}}</h2>
    <button v-on:click="clickTest">点击</button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      msg: 'hello from component a！'
    }
  },
  props: ['msgFromFather'],
  methods: {
    clickTest: function () {
      this.$emit("childSay", this.msg);//这块一定要写this.$emit
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
</style>
