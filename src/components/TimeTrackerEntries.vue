<template>
  <div id="entries">
    <b-table striped :items="items" :fields="fields">

      <template slot="actions" scope="row">
        <!-- We use click.stop here to prevent a 'row-clicked' event from also happening -->
        <b-btn size="sm" @click.stop="edit(row.item)">Edit</b-btn>

        <b-btn size="sm" @click.stop="remove(row.item)">x</b-btn>
      </template>
    </b-table>
  </div>


</template>


<script>
  export default {
    props: ['items'],
    data: function() {
      return {
        fields: {
          date: {label: 'Datum', sortable: true},
          start_time: {label: 'Startzeit', sortable: true},
          end_time: {label: 'Endzeit', sortable: true},
          description: {label: 'Beschreibung', sortable: true},
          actions: {label: 'Actions'}
        }
      }
    },
    methods: {
      edit: function(item) {
        this.$emit('edit', item)
      },
      remove: function(item) {
        this.$emit('remove', item)
      }
    }
  }
</script>
