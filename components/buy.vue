<template>
  <v-row class="justify-center">
    <v-dialog v-model="dialog" persistent max-width="800px">
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
              <v-col cols="6">
                <v-row>
                  <v-col cols="12">
                    <div>
                      <v-img :src="product.image" max-height="300"></v-img>
                    </div>
                    <div class="subtitle-1">
                      <b>Nama produk</b>
                    </div>
                    <div>{{ product.productName.charAt(0).toUpperCase() + product.productName.substring(1) }}</div>
                    <div class="subtitle-1">
                      <b>Bahan</b>
                    </div>
                    <div>{{ product.material}}</div>
                    <div class="subtitle-1">
                      <b>Size</b>
                    </div>
                    <div>{{ product.size }}</div>
                    <div class="subtitle-1">
                      <b>Total dibayar</b>
                    </div>
                    <div>Rp. {{ product.price }}</div>
                  </v-col>
                  <v-col cols="12">
                    <div>Cara pesan :</div>
                    <div>1. Masukkan data diri dan alamat lengkap</div>
                    <div>
                      2. Transfer ke rekening
                      <b>0240344254</b> a/n
                      <b>Hello world</b>
                    </div>
                    <div>3. Upload bukti transfer dibawah</div>
                    <div>4. Tunggu email konfirmasi dari admin kami</div>
                  </v-col>
                </v-row>
              </v-col>
              <v-col cols="6">
                <v-row>
                  <v-col cols="12">
                    <v-text-field v-model="username" label="Username*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field v-model="name" label="Nama*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field v-model="email" label="Email*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field v-model="address" label="Alamat Lengkap*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field v-model="postal" label="Kode Pos*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-file-input
                      v-model="paymentProof"
                      accept="image/*"
                      label="Upload Bukti Transfer"
                    ></v-file-input>
                  </v-col>
                </v-row>
                <small>*pesanan akan dikirim sesuai alamat yang tertera</small>
              </v-col>
            </v-row>
          </v-container>
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
	import cookies from 'js-cookie'

	export default {
		name: 'buy',
		props: ['product'],
		data: () => ({
			dialog: false,
			username: cookies.get('login')
				? JSON.parse(cookies.get('login')).username
				: '',
			name: cookies.get('login') ? JSON.parse(cookies.get('login')).name : '',
			address: cookies.get('login')
				? JSON.parse(cookies.get('login')).address
				: '',
			email: cookies.get('login') ? JSON.parse(cookies.get('login')).email : '',
			postal: '',
			paymentProof: null,
		}),
		methods: {
			handleBuy: function() {
				this.dialog = false
				let { productName, price } = this.product

				const data = this.$axios({
					method: 'POST',
					url: `${process.env.apiUrl}/orders`,
					data: {
						productName,
						price,
						username: this.username,
						name: this.name,
						address: this.address,
						postal: this.postal,
						email: this.email,
						paymentProof: this.paymentProof.name,
						date: moment().format('DDMMYYYY'),
					},
				})
					.then(response => {
						console.log('success order')
					})
					.catch(err => {
						console.log(err)
					})
			},
		},
	}
</script>
<style lang="scss" scoped>
.bold {
	font-weight: 900;
}
</style>