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
              <b-form-input placeholder="Datum" :disabled="timer.running == true" @keyup.enter="save(item)" v-model="item.date"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-1">
            <b-form-group label="Startzeit" label-text-align="left">
              <b-form-input placeholder="Startzeit" :disabled="timer.running == true" @keyup.enter="save(item)" v-model="item.start_time"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-1">
            <b-form-group label="Endzeit" label-text-align="left">
              <b-form-input placeholder="Endzeit" :disabled="timer.running == true" @keyup.enter="save(item)" v-model="item.end_time"></b-form-input>
            </b-form-group>
          </div>

          <div class="col-8">
            <b-form-group label="Beschreibung" label-text-align="left">
              <b-form-input placeholder="Beschreibung" @keyup.enter="save(item)" v-model="item.description"></b-form-input>
            </b-form-group>
          </div>
        </b-form>
      </div>

    <div v-if="timer.running === true">
      Timer läuft.

      <p>
        {{ hours }} Stunden {{ minutes }} Minuten {{ seconds }} Sekunden
      </p>

    </div>

    <template slot="footer">
      <b-button variant="primary" @click="save(item)">{{ this.item.id != undefined  ? "Ändern" : "Neu anlegen" }}</b-button>
      <b-button variant="secondary" @click="toggleTimer">{{ timer.running ? "Stopp" : "Start" }}</b-button>

    </template>

  </b-card>
  </div>

</template>

<script>
  var moment = require('moment');

  export default {
    props: {
      item: {
        default: function() { return { date: '', start_time: '', end_time: '', description: '' }}
      }
    },
    data: function() {
      return {
        now: Math.trunc((new Date()).getTime() / 1000),
        timer: {
          running: false,
          start_time: 0,
        }
      }
    },
    computed: {
      seconds() {
        return Math.trunc((this.now - this.timer.start_time) % 60);
      },
      minutes() {
        return Math.trunc(((this.now - this.timer.start_time) / 60) % 60);
      },
      hours() {
        return Math.trunc(((this.now - this.timer.start_time) / 60 / 60) % 60);
      }
    },
    methods: {
      save: function(item) {
        this.$emit('save', item);
      },
      startTimer: function () {
        this.timer.running = true;

        this.timer.start_time = this.now;
        this.item.start_time  = moment.unix(this.timer.start_time).format('HH:mm');

        window.setInterval(() => {
          this.now = Math.trunc((new Date()).getTime() / 1000);
          this.item.end_time = moment().format('HH:mm')
        }, 1000);
      },
      stopTimer: function () {
        this.timer.running = false;

        this.item.end_time = moment(this.now * 1000).format('HH:mm')


        alert("Stoping timer at " + moment(this.now))
        window.clearInterval(1000);
      },
      toggleTimer: function () {
        if (this.timer.running) {
          this.stopTimer();
        } else {
          this.startTimer();
        }
      }
    }
  }
</script>
