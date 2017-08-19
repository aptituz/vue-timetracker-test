<template>
  <div id="app">
    <time-tracker-entry-input v-on:save="updateItem" ></time-tracker-entry-input>
    <hr>
    <time-tracker-entries :items="items"></time-tracker-entries>
  </div>
</template>

<script>
import TimeTrackerEntryInput from './components/TimetrackerEntryInput.vue'
import TimeTrackerEntries from './components/TimetrackerEntries.vue'

export default {
  name: 'app',
  data: function(){
    return {
     items: [],
    }
  },
  components: {
    TimeTrackerEntryInput,
    TimeTrackerEntries
  },
  methods: {
    updateItem: function(item) {
      alert("updating")
      this.items.push(item);
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
</style>
