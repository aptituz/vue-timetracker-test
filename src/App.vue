<template>
  <div id="app">
    <time-tracker-entry-input v-bind:item="item" v-on:save="updateItem" ></time-tracker-entry-input>
    <hr>
    <time-tracker-entries v-on:edit="editItem" v-on:remove="removeItem" :items="items"></time-tracker-entries>
  </div>
</template>

<script>
import TimeTrackerEntryInput from '../src/components/TimetrackerEntryInput.vue'
import TimeTrackerEntries from '../src/components/TimeTrackerEntries.vue'

var moment = require('moment');

export default {
  name: 'app',
  data: function(){
    return {
      id: 0,
      items: [],
      item: this.newItem()
    }
  },
  components: {
    TimeTrackerEntryInput,
    TimeTrackerEntries
  },
  methods: {
    newItem: function() {
      return {
        date:       moment().format('D.M.Y'),
        start_time: moment().format('HH:MM'),
        end_time:   moment().add('15', "m").format('HH:MM'),
        description: ''
      }
    },
    editItem: function(item) {
      this.item = item
    },
    removeItem: function(item) {
      index = indexOf(item);
      this.items.splice(index, 1)
    },
    updateItem: function(item) {
      this.item = this.newItem();

      var index = this.items.indexOf(item);
      let updated_item = {
        id: item.id || this.id++,
        date: item.date,
        start_time: item.start_time,
        end_time: item.end_time,
        description: item.description
      };

      if (index !== -1) {
        this.items[index] = updated_item;
      } else {
        this.items.push(updated_item);
      }
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
