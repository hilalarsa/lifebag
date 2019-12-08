<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="400px">
      <template v-slot:activator="{ on }">
        <v-btn text dark v-on="on">Signup</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Signup</span>
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
          <v-btn color="blue darken-1" text @click="handleSignup">Signup</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
	import jwt from 'jsonwebtoken'
	export default {
		name: 'signup',
		data: () => ({
			dialog: false,
			username: '',
			password: '',
		}),
		methods: {
			handleSignup: function() {
				this.dialog = false
				console.log(this.username, this.password)

				let token = jwt.sign(
					{ token: this.username + this.password },
					process.env.privateKey
				)
				const data = this.$axios({
					method: 'POST',
					url: `${process.env.apiUrl}/users`,
					data: {
						username: this.username,
						password: this.password,
						role: 'user',
						token: token,
					},
				})
					.then(response => {
						console.log('success signup')
					})
					.catch(err => {
						console.log(err)
					})
			},
		},
	}
</script>