<template>
    <v-row class="justify-center">
      <v-col cols="8" >
        <v-card class="mx-auto" max-width="100%" >
          <v-img :src="productData.image" height="500px"></v-img>

          <v-card-title>{{ productData.productName.charAt(0).toUpperCase() + productData.productName.substring(1) }}</v-card-title>

          <v-card-subtitle>{{ productData.price }} | {{ productData.material }} | {{ productData.size }}</v-card-subtitle>

          <v-card-actions>
            <buy :product="productData"></buy>

            <v-btn color="purple" text @click="show = !show">About</v-btn>

            <v-spacer></v-spacer>

            <v-btn icon @click="show = !show">
              <v-icon>{{ show ? 'mdi-chevron-up' : 'mdi-chevron-down' }}</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>

              <v-card-text>{{ productData.about }}</v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
      </v-col>
    </v-row>
</template>
<script>
	import buy from '~/components/buy'

	export default {
		async asyncData({ req, res, params, $axios }) {
			const productData = await $axios.$get(
				`${process.env.apiUrl}/products/${params.id}`
			)
			console.log(productData)
			return { productData }
        },
        components:{
            buy
        },
		data: () => ({
			show: false,
		}),
	}
</script>