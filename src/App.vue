<template>
  <div id='app' class='container'>
    <div v-for='(day, index) in weekdays' :key='index' class='weekdays'>
      <h1>{{ day | capitalize }}</h1>
      <profile :group='group[index]'></profile>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Profile from './components/Profile.vue'

export default {
  name: 'app',
  components: {
    Profile
  },
  data () {
    return {
      data: [],
      weekdays: ['sun', 'mon', 'tue', 'wed', 'thu', 'fri', 'sat'],
      group: [[], [], [], [], [], [], []],
      errors: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      axios.get('https://uinames.com/api/?ext&amount=25').then(response => {
        this.data = response.data
        this.setGroup()
      }).catch(e => {
        this.errors.push(e)
      })
    },
    setGroup () {
      this.data.forEach(item => {
        let day = this.getDayOfWeek(item.birthday.mdy)
        this.group[day].push(item)
      })
    },
    getDayOfWeek (mdy) {
      let d = new Date(mdy)
      return d.getDay()
    }
  },
  filters: {
    capitalize: function (value) {
      return value.toUpperCase()
    }
  }
}
</script>

<style>
.container {
  display: flex;  
}
.weekdays {
  text-align: center
}
</style>
