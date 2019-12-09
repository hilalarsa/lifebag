<template>
  <section>
    <v-flex xs12>
      <v-container grid-list-xl>
        <v-layout row wrap align-center>
          <v-flex v-for="(item, index) in productData" v-bind:key="index" xs12 md4>
            <v-card flat class="transparent">
              <v-card-text class="text-center">
                <v-img :src="item.image" width="100%" max-height="200px" />
              </v-card-text>
              <hr />
              <v-card-title primary-title class="layout justify-center">
                <div class="headline text-center">{{ item.productName.charAt(0).toUpperCase() + item.productName.substring(1) }}</div>
              </v-card-title>
              <v-card-text primary-title class="layout">
                <div>Rp. {{ item.price }} | {{ item.material }} | {{ item.size }}</div>
              </v-card-text>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-flex>
  </section>
</template>
<script>
	export default {
		data() {
			return {
				title: 'Lifebag Studio',
			}
		},
		async asyncData({ req, res, params, $axios }) {
			const productData = await $axios.$get('http://localhost:3001/products')
			return { productData }
		},
	}
</script>