<template>
  <v-row>
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
                  <div>Cara pesan : </div>
                  <div>1. Masukkan data </div>
                  <div>2. Transfer </div>
                  <div>3. Kirim bukti transfer </div>
                  <div>4. Tunggu email konfirmasi </div>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="username" label="Nama*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" label="Alamat Lengkap*" type="password" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field v-model="password" label="Upload Bukti Transfer" type="password" required></v-text-field>
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
  export default {
    name:"buy",
    data: () => ({
      dialog: false,
    }),
    methods: () => ({
      handleBuy(){
        this.dialog=false
        // this.username
        // this.password
      }
    })
  }
</script>