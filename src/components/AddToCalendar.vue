<template>
  <button @click="addToCalendar">{{ buttonText }}</button>
</template>

<script>
/* eslint-disable no-console */
import 'whatwg-fetch';

export default {
  name: 'AddToCalendar',
  props: {
    buttonText: { type: String, default: "Add to calendar" },
    details: { type: String },
    endTime: { type: Date, required: true },
    location: { type: String },
    startTime: { type: Date, required: true },
    summary: { type: String, required: true },
  },

  data() {
    return {
      googleCalendarLink: null,
      
      dataSource : {
        load :(options) => this.getData(options, { ShowDeleted : false}),
      }
      
    }
  },

  methods: {
    addToCalendar() {
      if(!this.startTime) return console.warn("prop: startTime is required");
      if(!this.endTime) return console.warn("prop: endTime is required");
      if(!this.summary) return console.warn("prop: summary is required");
      this.googleCalendarLink = `http://www.google.com/calendar/event?action=TEMPLATE&text=${this.summary || ""}&dates=${this.formatDate(this.startTime)}/${this.formatDate(this.endTime)}&details=${this.details || ""}&location=${this.location || ""}`
      window.open(this.googleCalendarLink),
      console.log(this.googleCalendarLink) 
    },
    
    request() {
      // eslint-disable-next-line no-undef
      gapi.client.calendar.events.insert({
        'calendarId': 'primary'
      });
    },

    

    getData(_, requestOptions) {
      const API_KEY = 'AIzaSyArWCVzkBsh0Q8NKKEVS6SRkmuGLY7bj9Q';
      const CLIENT_ID ='681960233511-iuqgg3rjemh3sv8nurlisdp6bajc2dou.apps.googleusercontent.com';
      const dataUrl = ['https://www.googleapis.com/calendar/v3/calendars/eimon221996@gmail.com/events',
        CLIENT_ID, '/events?key=', API_KEY].join('');

      return fetch(dataUrl, requestOptions).then(
        (response) => response.json(),
      ).then((data) => data.items);
    },

    formatDate(date) {
      const day = date.getDate();
      const monthIndex = date.getMonth();
      const year = date.getFullYear();

      const hour = date.getHours();
      const minutes = date.getMinutes();

      let formatted_date;
      if(hour === 0 && minutes === 0) {
        formatted_date = ("" + year) + this.zero_pad2(monthIndex + 1) + this.zero_pad2(day);
      } else {
        formatted_date = ("" + year) + this.zero_pad2(monthIndex + 1) + this.zero_pad2(day) + "T" + this.zero_pad2(hour) + this.zero_pad2(minutes) + "00Z";
      }

      return formatted_date;
    },

    zero_pad2(num) {
      if(num < 10) return "0" + num;
        return num;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

