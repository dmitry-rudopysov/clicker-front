<template>
  <div id="score">
    <div class="cross" id="griffindor" @click="addScore">
    </div>
    <div class="cross" id="slytherin" @click="addScore">
    </div>
    <div class="cross" id="hufflepuff" @click="addScore">
    </div>
    <div class="cross" id="ravenclaw" @click="addScore">
      <!--<div v-if="user">-->
        <!--<h1>Hello USER!</h1>-->
        <!--<img :src="user.photoURL" width="100"> <br>-->
        <!--<h3>{{user.displayName}}</h3>-->
        <!--<p>{{user.email}}</p>-->
        <!--<button @click="logOut">Log out</button>-->
        <!--<br><br><br>-->
        <!--<pre>{{user}}</pre>-->
      <!--</div>-->
    </div>
  </div>
</template>

<script>
import auth from '@/auth'
import axios from 'axios'

export default {
  name: 'auth-success',
  computed: {
    user () {
      return this.$store.getters['user/user']
    }
  },
  methods: {
    logOut () {
      auth.logout()
    },
    addScore (event) {
      let targetId = event.currentTarget.id
      let config = {
        headers: {
          'Content-type': 'application/json'
        }
      }
      console.log(targetId) // returns 'foo'
      console.log(this.user.uid)
      const str = JSON.stringify({
        'addScore': 10,
        'teamName': targetId,
        'userId': this.user.uid})
      axios
        .post('http://localhost:8080/addAward', str, config)
        .then((response) => {
          console.log(response)
        }
        )
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>
<style>
  html, body {
    height: 100%;
    padding: 0;
    margin: 0;
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
  }

  .cross {
    background-size: 100%;
  }
</style>
