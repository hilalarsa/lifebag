<template>
  <v-row class="justify-center">
    <v-dialog v-model="dialog" persistent max-width="400px">
      <template v-slot:activator="{ on }">
        <v-btn text dark v-on="on">Buy</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Buy</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <div>Cara pesan :</div>
                <div>1. Masukkan data</div>
                <div>2. Transfer</div>
                <div>3. Kirim bukti transfer</div>
                <div>4. Tunggu email konfirmasi</div>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="username" label="Nama*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="address" label="Alamat Lengkap*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-file-input
                  v-model="paymentProof"
                  accept="image/*"
                  label="Upload Bukti Transfer"
                ></v-file-input>
              </v-col>
            </v-row>
          </v-container>
          <small>*pesanan akan dikirim sesuai alamat yang tertera</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
          <v-btn color="blue darken-1" text @click="handleBuy">Kirim Pesanan</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>
<script>
	import moment from 'moment'
	export default {
		name: 'buy',
		props: ['product'],
		data: () => ({
			dialog: false,
			username: '',
			address: '',
      paymentProof: null,
      imageName:'',
      imageFile:'',
      imageUrl:'',
		}),
		methods: {
			handleBuy: function() {
				this.dialog = false
				let { productName, price } = this.product
				// console.log(moment())
        console.log(this.paymentProof.name)
        console.log(this.username, this.address)
				const data = this.$axios({
					method: 'POST',
					url: `${process.env.apiUrl}/orders`,
					data: {
						productName,
						price,
						username: this.username,
						address: this.address,
						paymentProof: this.paymentProof.name,
						date: moment().format("DDMMYYYY"),
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