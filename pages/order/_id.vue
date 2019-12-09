<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">Nama produk</th>
          <th class="text-left">Harga</th>
          <th class="text-left">Username</th>
          <th class="text-left">Email</th>
          <th class="text-left">Nama Lengkap</th>
          <th class="text-left">Alamat Lengkap</th>
          <th class="text-left">Kode Pos</th>
          <th class="text-left">Bukti pembayaran</th>
          <th class="text-left">Tanggal</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,index) in orderData" :key="index">
          <td>{{ item.productName.charAt(0).toUpperCase() + item.productName.substring(1) }}</td>
          <td>{{ item.price }}</td>
          <td>{{ item.username }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.address }}</td>
          <td :href="item.paymentProof">{{ item.paymentProof ? "Sudah upload" : "Belum upload" }}</td>
          <td>{{ item.date }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>
<script>
	import cookies from 'js-cookie'

	export default {
		async asyncData({ req, res, params, $axios }) {
			const orderData = await $axios.$get(`${process.env.apiUrl}/orders`)
			console.log(orderData)
			return { orderData }
		},
		mounted() {
			if (
				cookies.get('login') &&
				JSON.parse(cookies.get('login')).role == 'admin'
			) {
				console.log('Welcome admin')
			} else {
				this.$router.push('/')
			}
		},
	}
</script>