<template>
<md-card>
<div>
  <md-card-header>
    <md-card-header-text>
      <div class="md-subhead">{{cityName}}</div>
      <div>{{country}}</div>
      <div>MAX : {{day.temp.max}}</div>
      <div>MIN : {{day.temp.min}}</div>
    </md-card-header-text>

    <md-card-media md-medium>
      <img src="../assets/card-weather.png" alt="People">
    </md-card-media>
  </md-card-header>
  
  <md-card-actions>
    <md-button>Action</md-button>
    <md-button>Action</md-button>
  </md-card-actions>
  </div>
</md-card>
</template>

<script>
export default {
  props: ['day', 'cityName', 'country'],
  data () {
    return {
    }
  },
  watch: {
  },
  computed: {
  },
  methods: {
  }
}
</script>

