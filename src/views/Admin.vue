<template v-if="this.currentRole==='ADMIN'">
  <div>
    <h1>Hello {{admin.displayName}}!</h1>
    Your current role {{currentRole}}

    <ul>
      <li v-for="user in users" :key="user.uid">
        {{ user.displayName }} {{ user.email }} {{ user.mark }} {{ user.role }}
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'
import auth from '@/auth'
import config from '../config.js'

export default {
  name: 'Admin',
  methods: {
    logOut () {
      auth.logout()
    }
  },
  computed: {
    admin () {
      return this.$store.getters['user/user']
    }
  },
  data: function () {
    return {
      users: [],
      currentRole: '',
      config: {
        headers: {
          'Content-type': 'application/json'
        }
      }
    }
  },
  watch: {
    // эта функция запускается при любом изменении admin
    admin: function () {
      console.log(this.admin.uid)
      axios
        .get(config.url + 'admin/getRole?uid=' + this.admin.uid, this.config)
        .then((response) => {
          this.currentRole = response.data
        }
        )
        .catch((error) => {
          console.log(error)
        })

      axios
        .get(config.url + 'admin/getAllUsers?uid=' + this.admin.uid, this.config)
        .then((response) => {
          this.users = response.data
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
  body {
    background-color: white;
  }

</style>
