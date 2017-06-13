<template>
<div class="app-viewport" id="file-list">
  <md-whiteframe md-elevation="5" class="main-toolbar">
    <md-toolbar class="md-large">
        <span class="main-title">Weather APP</span>
    </md-toolbar>
  </md-whiteframe>
  <typeahead></typeahead>
  
</div>
</template>

<script>
import Typeahead from './components/Typeahead'

export default {
  name: 'app',
  components: {
    Typeahead
  },
  data () {
    return {
    }
  }
}

</script>

<style>
html,
body,
.app-viewport {
  height: 100%;
  overflow: hidden;
}

.app-viewport {
  display: flex;
  flex-flow: column;
}

.main-toolbar {
  position: relative;
  z-index: 10;
}

.main-content {
  position: relative;
  z-index: 1;
  overflow: auto;
}

.main-title{
  font-size: 35px;
}

</style>
