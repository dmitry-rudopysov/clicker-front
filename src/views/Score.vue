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
        .get('http://localhost:8080/getScore')
        .then(response => (this.info = response.data))
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  /*h3 {*/
  /*margin: 40px 0 0;*/
  /*}*/

  /*ul {*/
  /*list-style-type: none;*/
  /*padding: 0;*/
  /*}*/

  /*li {*/
  /*display: inline-block;*/
  /*margin: 0 10px;*/
  /*}*/

  /*a {*/
  /*color: #42b983;*/
  /*}*/

 /*#score { height: 100%; width: 100%; padding: 0; margin: 0; }*/
  html, body { height: 100%; padding: 0; margin: 0; }
  .cross { width: 50%; height: 50%; float: left; }
  #score {
    height: 100%;
    padding: 0;
    margin: 0;
    background: no-repeat url('../assets/hp.png');
    background-size: contain;
    background-position-x: center;
    font-family:    Harry,fantasy;
    font-size:      250px;
    text-align: center;
    vertical-align: middle;
    color: rgba(255, 255, 255, 0.8);
  }
  #div1 { background-size: 100%;}
  #div2 { background-size: 100%;}
  #div3 { background-size: 100%;}
  #div4 { background-size: 100%;}

  @font-face {
    font-family: "Harry";
    src: url('../assets/hp.ttf');
  }

</style>
