<template>
  <v-app light>
    <!--The SideMenu Component go here-->
    <v-toolbar fixed app light clipped-left color="primary" class="elevation-2">
      <v-toolbar-side-icon @click="drawer = !drawer"  class="white--text"></v-toolbar-side-icon>
      <v-toolbar-title class="white--text">News App</v-toolbar-title>
    </v-toolbar>

    <v-content>
      <v-container fluid>
        <MainContent :articles="articles"></MainContent> <!-- Add the component in the template -->
      </v-container>
    </v-content>
    <v-footer class="secondary" app>
      <v-layout row wrap align-center>
        <v-flex xs12>
          <div class="white--text ml-3">
            Made with
            <v-icon class="red--text">favorite</v-icon>
            by <a class="white--text" href="https://vuetifyjs.com" target="_blank">Vuetify</a>
            and <a class="white--text" href="https://github.com/rachidsakara"
                   target="_blank">Rachid Sakara</a>
          </div>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>


</template>

<script>

  import axios from 'axios' // importing the axios (a HTTP library) to connects the app with the News API
  import MainContent from './components/MainContent.vue' // import the Main Content component

  export default {

    components: {
      MainContent, // Register the component
    },

    data() {
      return {
        drawer: false, // false = Vuetify automatically "do the right thing" to show/hide the drawer
        api_key:'Your_API_KEY_HERE', // Your API Key go here
        articles: [],
        errors: []
      }
    },
    created () {
      axios.get('https://newsapi.org/v2/top-headlines?sources=techcrunch&apiKey='+this.api_key)
        .then(response => {
          //this.articles = response.data.articles
          this.articles = response.data.articles
          console.log('data:')
          console.log(response.data.articles) // This will give you access to the full object
        })
        .catch(e => {
          this.errors.push(e)
        })
    },


  }
</script>
