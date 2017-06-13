<template>
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
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Optio itaque ea, nostrum odio. Dolores, sed accusantium quasi non, voluptas eius illo quas, saepe voluptate pariatur in deleniti minus sint. Excepturi.
    </md-card-content>
  </md-card-expand>
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

</style>

