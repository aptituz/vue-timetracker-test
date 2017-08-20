<template>
  <div class="container-fluid align-items-center timetracking-input">

  <b-card title="Zeit erfassen" class="justify-content-center">
      <p class="card-text muted">
        In der untenstehenden Form können Zeiten erfasst oder bearbeitet werden.
      </p>
      <div class="align-items-center align-self-center">
        <b-form class="row">
          <div class="col-1">
            <b-form-group label="Datum" label-text-align="left">
              <b-form-input placeholder="Datum" @keyup.enter="save(item)" v-model="item.date"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-1">
            <b-form-group label="Startzeit" label-text-align="left">
              <b-form-input placeholder="Startzeit" @keyup.enter="save(item)" v-model="item.start_time"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-1">
            <b-form-group label="Endzeit" label-text-align="left">
              <b-form-input placeholder="Endzeit" @keyup.enter="save(item)" v-model="item.end_time"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-8">
            <b-form-group label="Beschreibung" label-text-align="left">
              <b-form-input placeholder="Beschreibung" @keyup.enter="save(item)" v-model="item.description"></b-form-input>
            </b-form-group>
          </div>
        </b-form>
      </div>

    <template slot="footer">
      <b-button variant="primary" @click="save(item)">{{ this.item.id != undefined  ? "Ändern" : "Neu anlegen" }}</b-button>
    </template>

  </b-card>
  </div>

</template>

<script>
  export default {
    props: {
      item: {
        default: function() { return { date: '', start_time: '', end_time: '', description: '' }}
      }
    },
    methods: {
      save: function(item) {
        this.$emit('save', item);
      }
    }
  }
</script>
