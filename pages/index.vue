<template>
  <section class="container">
    <!--<img src="~assets/img/logo.png" alt="Nuxt.js Logo" class="logo"/>-->
    <app-logo/>
    <h1 class="title">
      USERS
    </h1>
    <ul class="users">
      <li v-for="(user, index) in users" :key="index" class="user">
        <nuxt-link :to="{ name: 'id', params: { id: index }}">
          {{ user.name }}
        </nuxt-link>
      </li>
    </ul>
  </section>
</template>

<script>
  import axios from '~/plugins/axios'
  import AppLogo from '~/components/AppLogo.vue'

  export default {
    async asyncData () {
      let formData = {}
      let { data } = await axios.get('/api/users')
      let { testAccount } = await axios.get('/api/testAccountList')

      formData.users = data
      formData.testList = testAccount

      console.log(formData)
      return formData
    },
    head () {
      return {
        title: 'Users'
      }
    },
    components: {
      AppLogo
    }
  }
</script>

<style scoped>
  .title {
    margin: 30px 0;
  }

  .users {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .user {
    margin: 10px 0;
  }
</style>
