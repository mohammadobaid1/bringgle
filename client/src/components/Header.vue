<template lang="pug">
  md-toolbar.md-primary(md-elevation="2")
    h3.md-title(style="flex: 1")
      router-link(to="/")
        img#logo(src="../assets/logo-alt.svg" alt="Bringgle" height="60") 
    md-menu.md-xsmall-hide(md-direction="bottom-end" v-show="user && user.name")
      md-button(md-menu-trigger)
        i.fa.fa-user
        | {{ user.name }}
      md-menu-content
        md-menu-item( v-on:click='logOut()') Log out
    md-button.md-xsmall-hide
      router-link(to="/create")
        i.fa.fa-plus
        | Create list
    md-menu.md-xsmall-show(md-direction="bottom-end")
      md-button.md-icon-button(md-menu-trigger)
        i.fa.fa-ellipsis-v
      md-menu-content
        router-link(to="/create")
          md-menu-item Create List
        md-menu-item( v-on:click='logOut()') Log out
</template>

<script lang="ts">
import router from '../router'
import CookiesUtils from '../cookies';

export default {
  name: 'Header',
  data: function () {
    return {
      user: {}
    }
  },
  mounted: function () {
    this.user = this.$store.state.currentUser
  },
  methods: {
    logOut () {
      CookiesUtils.removeUser()
      router.push('/')
    }
  }
}
</script>

<style scoped>
  a, .md-theme-default a:not(.md-button) {
    color: white;
  }
  #logo {
    height: 40px;
  }
</style>
