<template>
  <v-row class="justify-end">
    <v-dialog v-model="dialog" persistent max-width="400px">
      <template v-slot:activator="{ on }">
        <v-btn text dark v-on="on">Login</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Login</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field v-model="username" label="Username*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" label="Password*" type="password" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
          <v-btn color="blue darken-1" text @click="handleLogin">Login</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
	import jwt from 'jsonwebtoken'
	import cookies from 'js-cookie'

	export default {
		name: 'login',
		data: () => ({
			dialog: false,
			username: '',
			password: '',
		}),
		methods: {
			handleLogin: function() {
				// this.dialog = false
				console.log(this.username, this.password)
				const data = this.$axios({
					method: 'GET',
					url: `${process.env.apiUrl}/users?username=${this.username}`,
				})
					.then(response => {
						let { username, password, token, address, email, role, name } = response.data[0]

						if (username == this.username && password == this.password) {
							let verify = jwt.verify(token, process.env.privateKey)
							if (verify.token) {
								console.log('Login succes, redirecting...')
								cookies.set('login', {
									username,
									token,
									address,
									email,
									role,
									name
								}, { expires: 7 })
								this.$router.push('/')
							} else {
								console.log('JSON web token malformed')
							}
						} else {
							console.log('username pass wrong')
						}
					})
					.catch(err => {
						console.log(err)
					})
			},
		},
	}
</script>