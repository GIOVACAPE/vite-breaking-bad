<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import { store } from './store.js';


export default {
  name: "App",
  components: {
    AppHeader,
    AppMain
  },
  data() {
    return {
      card: [],
      choose: 'Alien',
      link: '',
      store
    }
  },
  created() {
    this.link = "https://db.ygoprodeck.com/api/v7/cardinfo.php"
    this.store.loading = true;
    axios
      .get(this.link)
      .then((response) => {
        this.store.card = response.data.data.slice(0, 18)
        this.store.loading = false;
      });
  },
}

</script>

<template>

  <AppHeader />
  <AppMain />

</template>

<style lang="scss">
@import './styles/main.scss'
</style>
