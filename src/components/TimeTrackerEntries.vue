<template>
  <div id="entries">
    <b-table striped :items="items" :fields="fields">
    </b-table>
  </div>
</template>


<script>
  export default {
    props: ['items'],
    data: function() {
      return {
          fields: {
            date: { label: 'Datum', sortable: true },
            start_time: { label: 'Startzeit', sortable: true },
            end_time: { label: 'Endzeit', sortable: true },
            description: { label: 'Beschreibung', sortable: true }
          }
      }
    }
  }
</script>
