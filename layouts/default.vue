<template>
<v-app light>
  <v-content>
    <template>
      <v-card class="overflow-hidden">
        <v-app-bar
          absolute
          color="#43a047"
          dark
          shrink-on-scroll
          prominent
          src="https://picsum.photos/1920/1080?random"
          fade-img-on-scroll
          scroll-target="#scrolling-techniques-5"
          scroll-threshold="500"
        >
          <template v-slot:img="{ props }">
            <v-img
              v-bind="props"
              gradient="to top right, rgba(55,236,186,.7), rgba(25,32,72,.7)"
            ></v-img>
          </template>

          <v-app-bar-nav-icon></v-app-bar-nav-icon>

          <v-toolbar-title>Life-bag</v-toolbar-title>

          <v-spacer></v-spacer>

          <login></login>

          <v-btn text>
            Sign up
          </v-btn>

        </v-app-bar>
        <v-sheet
          id="scrolling-techniques-5"
          class="overflow-y-auto"
          max-height="600"
        >
			<nuxt class="main"/>
        </v-sheet>
      </v-card>
    </template>
    <v-footer color="blue darken-2">
        <v-layout row wrap align-center>
          <v-flex xs12>
            <div class="white--text ml-4">
              Lifebag
              <v-icon class="red--text">mdi-heart</v-icon>
            </div>
          </v-flex>
        </v-layout>
      </v-footer>
    </v-content>
</v-app>
</template>

<script>
import login from '~/components/login'
export default {
  components:{
    login
  },
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Lifebag Malang'
    }
  }
}
</script>
<style lang="scss" scoped>
.main{
	margin-top:100px
}
</style>