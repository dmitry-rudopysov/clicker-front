<template>
  <div>
    <li v-for="item in info.teams">
      {{ item.name }} - {{ item.score }}
    </li>
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
        .get('http://ithogwarts.com/api/getScore')
        .then(response => (this.info = response.data))
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
