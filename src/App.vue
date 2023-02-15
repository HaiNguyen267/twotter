<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twotter
        </div>
      </router-link>
      <div class="navigation__user">
        HaiNguyen
      </div>
    </nav>
    <UserProfile />
  </div>
</template>

<script>
import UserProfile from './components/UserProfile.vue'

export default {
  name: 'App',
  components: { UserProfile }
}
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
}

nav {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  position: fixed;
  // width: 100vw;
  top: 0;
  left: 0;
  right: 0;
  background: rgb(12, 175, 72);
  height: 50px;
  color: white;
  font-size: 1.3em;
  display: flex;
  padding: 10px 30px;
  justify-content: space-between;
  align-items: center;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: rgb(236, 236, 236);
  display: flex;
  margin: 0;
  height: 100vh;
  padding: 20px;
  padding-top: 50px;

}

button {
  width: fit-content;
}
</style>
