<template>
  <div>
      <h1>{{message}}</h1>
      <h2>Counter will go here: {{ count }}</h2>
      <br>
      <button v-on:click="incrementCount">Increment Count</button>
  </div>
</template>

<script>
export default {
    name: "Counter",
    props: {
        message: String
    },
    data: function() {
        return {
            count: 0
        }
    },
    methods: {
        incrementCount() {
            this.count++;
        }
    }
}
</script>