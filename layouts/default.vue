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
              <v-img v-bind="props" gradient="to top right, rgba(55,236,186,.7), rgba(25,32,72,.7)"></v-img>
            </template>

            <v-app-bar-nav-icon></v-app-bar-nav-icon>

            <v-toolbar-title>Life-bag</v-toolbar-title>

            <v-spacer></v-spacer>

            <template v-if="isLoggedIn">
              <v-menu left bottom>
                <template v-slot:activator="{ on }">
                  <v-btn icon v-on="on">
                    <v-icon>mdi-account</v-icon>
                  </v-btn>
                </template>

                <v-list>
                  <v-list-item>
                    <v-list-item-title @click="handleLogout" class="pointer">Logout</v-list-item-title>
                  </v-list-item>
                </v-list>
              </v-menu>
            </template>

            <template v-else-if="!isLoggedIn">
              <login></login>
              <signup></signup>
            </template>
          </v-app-bar>
          <v-sheet id="scrolling-techniques-5" class="overflow-y-auto" max-height="600">
            <nuxt class="main" />
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
	import signup from '~/components/signup'

	import cookies from 'js-cookie'

	export default {
		components: {
			login,
			signup,
		},
		data() {
			return {
				isLoggedIn: cookies.get('login') ? true : false
			}
		},
		methods: {
			handleLogout: () => {
				console.log('logging out')
        cookies.remove('login')
        window.location.href = "/"
				// this.$route.push('/')
			},
		},
	}
</script>
<style lang="scss" scoped>
.main {
	margin-top: 128px;
}
.pointer {
	cursor: pointer;
}
</style>