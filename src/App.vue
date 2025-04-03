<template>
  <div id="app">
    <nav-bar />
    <aside-menu :menu="menu" />
    <router-view />
    <footer-bar />
  </div>
</template>

<script>
import { defineComponent } from 'vue'
// import menu from '@/menu.js'
import NavBar from '@/components/NavBar.vue'
import AsideMenu from '@/components/AsideMenu.vue'
import FooterBar from '@/components/FooterBar.vue'

export default defineComponent({
  name: 'AppComponent',
  components: {
    FooterBar,
    AsideMenu,
    NavBar
  },
  data () {
    return {
      menu: []
    }
  },
  mounted () {
    fetch('http://bag-sys.py:8084/api/v1/menu')
      .then(response => response.json())
      .then(data => {
        // console.log(JSON.stringify(data))
        this.menu = data
      }).catch(error => console.error('Error al obtener los datos:', error))
  },
  created () {
    this.$store.commit('user', {
      name: 'John Doe',
      email: 'john@example.com',
      avatar: 'https://avatars.dicebear.com/v2/gridy/John-Doe.svg'
    })
  }
})
</script>
