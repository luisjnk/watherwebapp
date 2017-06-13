<template>
    <md-list>
      <md-list-item>
        <md-card>
          <md-card-header>
            <div class="md-title">{{cityName}}</div>
            <div class="md-subhead">{{country}}</div>
            <div class="md-subhead">MAX : {{day.temp.max}}</div>
            <div class="md-subhead">MIN : {{day.temp.min}}</div>
            <div class="md-subhead">Date : {{day.dt}}</div>
          </md-card-header>

          <md-card-expand>
            <md-card-actions>
              <span style="flex: 1"></span>
              <md-button class="md-icon-button" md-expand-trigger>
                <md-icon>keyboard_arrow_down</md-icon>
              </md-button>
            </md-card-actions>

            <md-card-content>
             <md-layout :md-gutter="8">
              <md-layout>
                <span>Humidity</span>
                 &nbsp
                <span>{{day.humidity}}</span>
              </md-layout>

              <md-layout>
               <span>Pressure</span>
                &nbsp
                <span>{{day.pressure}}</span>
              </md-layout>

              <md-layout>
              <span>Speed</span>
               &nbsp
                <span>{{day.speed}}</span>
              </md-layout>
            </md-layout>
            </md-card-content>
          </md-card-expand>
        </md-card>
       </md-list-item>   
    </md-list>
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

<style>
.md-title {
  padding-left: 8px;
  color: #fff;
  background-color: cornflowerblue;
}
.md-list-action .md-icon {
  color: rgba(#000, .26);
}

.md-avatar-icon .md-icon {
  color: #fff !important;
}
.md-card {
      width: 100%;
}
</style>

