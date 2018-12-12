<template>
  <div id="score">
    <div class="cross" id="griffindor" @click="addScore">
    </div>
    <div class="cross" id="slytherin" @click="addScore">
    </div>
    <div class="cross" id="hufflepuff" @click="addScore">
    </div>
    <div class="cross" id="ravenclaw" @click="addScore">
    </div>
    <div class="footer">
      <button @click="logOut">Log out</button>
    </div>
  </div>
</template>

<script>
import auth from '@/auth'
import axios from 'axios'
import config from '../config.js'

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
      const str = JSON.stringify({
        'teamName': targetId,
        'userId': this.user.uid
      })
      axios
        .post(config.url + 'addAward', str, this.config)
        .then((response) => {
          this.$swal({
            title: 'Ваша оценка учтена',
            // html: 'I will close in <strong></strong> seconds.',
            timer: 2000,
            onBeforeOpen: () => {
              this.$swal.showLoading()
              // this.$swal.timerInterval = setInterval(() => {
              //   this.$swal.getContent().querySelector('strong')
              //     .textContent = this.$swal.getTimerLeft()
              // }, 100)
            },
            onClose: () => {
              clearInterval(this.$swal.timerInterval)
            }
          }).then((result) => {
            if (
              // Read more about handling dismissals
              result.dismiss === this.$swal.DismissReason.timer
            ) {
              console.log('I was closed by the timer')
            }
          })
          console.log(response)
        }
        )
        .catch((error) => {
          console.log(error)
        })
    }
  },
  mounted: function () {
    // Костыль, связанный с использованием firebase для oAuth
    const str = JSON.stringify({
      'uid': this.user.uid,
      'displayName': this.user.displayName,
      'email': this.user.email
    })

    axios
      .post(config.url + 'registerUser', str, this.config)
      .then((response) => {
        console.log(response)
      }
      )
      .catch((error) => {
        console.log(error)
      })
    /// костыль
  },
  data: function () {
    return {
      config: {
        headers: {
          'Content-type': 'application/json'
        }
      }
    }
  }
}
</script>
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
    background-size: 100%;
  }

  #score {
    height: 100%;
    padding: 0;
    margin: 0;
    padding-bottom: 9px;
  }

  #griffindor {
    background: no-repeat url('../assets/gryffindor.jpg');
    background-size: contain;
    background-position-x: center;
  }

  #slytherin {
    background: no-repeat url('../assets/slytherin.jpg');
    background-size: contain;
    background-position-x: center;
  }

  #hufflepuff {
    background: no-repeat url('../assets/hufflepuff.jpg');
    background-size: contain;
    background-position-x: center;
  }

  #ravenclaw {
    background: no-repeat url('../assets/ravenclaw.jpg');
    background-size: contain;
    background-position-x: center;
  }

  .footer {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 10px;
    background-color: black;
  }

  button {
    display:inline-block;
    padding:0.35em 1.2em;
    border:0.1em solid #FFFFFF;
    margin:0 0.3em 0.3em 0;
    border-radius:0.12em;
    box-sizing: border-box;
    text-decoration:none;
    font-family:'Roboto',sans-serif;
    font-weight:300;
    color:#000000;
    text-align:center;
    transition: all 0.2s;
  }

</style>
