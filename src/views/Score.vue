<template>
  <div id="score">
    <div class="cross" id="div1">
      {{info.teams[0].score}}
    </div>
    <div class="cross" id="div2">
      {{info.teams[1].score}}
    </div>
    <div class="cross" id="div3">
      {{info.teams[2].score}}
    </div>
    <div class="cross" id="div4">
      {{info.teams[3].score}}
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import config from '../config.js'

export default {
  name: 'Score',
  data: function () {
    return {
      info: String
    }
  },
  mounted () {
    this.apiRequest()
    this.time = setInterval(this.apiRequest, 1000)
  },
  methods: {
    apiRequest: function () {
      axios
        .get(config.url + '/getScore')
        .then(response => (this.info = response.data))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  html, body {
    height: 100%;
    padding: 0;
    margin: 0;
    background: #000000;
  }
  .cross {
    width: 50%;
    height: 50%;
    float: left;
  }
  #score {
    height: 100%;
    padding: 0;
    margin: 0;
    background: no-repeat url('../assets/hp.png');
    background-size: contain;
    background-position-x: center;
    font-family: Harry,fantasy;
    font-size: 250px;
    text-align: center;
    vertical-align: middle;
    color: rgba(255, 255, 255, 0.8);
  }

  @font-face {
    font-family: "Harry";
    src: url('../assets/hp.ttf');
  }

</style>
