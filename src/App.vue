<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <AddToCalendar
      :buttonText="buttonText"
      :summary="summary"
      :startTime="startTime"
      :endTime="endTime"
      :location="location"
      :details="details"
      
    />
    <!-- <example-calendar></example-calendar> -->
  </div>
</template>

<script>
import AddToCalendar from './components/AddToCalendar.vue'
// import ExampleCalendar from './components/AddToCalendar.vue'

export default {
  name: 'app',

  data() {
    return {
      buttonText: "Add to calendars",
      details: "this is testing of add to calendar component",
      location: "ruby tower, dadar",
      startTime: new Date('7/7/2022'),
      endTime: new Date('7/9/2022'),
      summary: "Event summary",
    }
  },

  components: {
    AddToCalendar,
    // ExampleCalendar
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
