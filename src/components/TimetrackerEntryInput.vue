<template>
  <div id="timetracking-input">
    <b-form inline.boolean="true">
      <b-form-input placeholder="Datum" v-model="item.date"></b-form-input>
      <b-form-input placeholder="Startzeit" v-model="item.start_time"></b-form-input>
      <b-form-input placeholder="Endzeit" v-model="item.end_time"></b-form-input>
      <b-form-input placeholder="Beschreibung" v-model="item.description"></b-form-input>
      <b-button variant="primary" @click="save(item)">Speichern</b-button>
    </b-form>
  </div>
</template>

<script>
  export default {
    props: {
      item: {
        default: function() { return { date: '', start_time: '', end_time: '', description: '' }}
      }
    },
    computed: {
      _item: function() { return this.item }
    },
    methods: {
      save: function(item) {
        this.$emit('save', Object.assign({}, item));
      }
    }
  }
</script>
