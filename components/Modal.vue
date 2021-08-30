<template>
  <v-dialog
    max-width="290"
    v-model="isDialogOpen"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-btn
        color="primary"
        dark
        v-bind="attrs"
        v-on="on"
      >
        Add New Freind Data
      </v-btn>
    </template>

    <v-card>
      <v-card-title class="text-h5">
        Add New Friend
      </v-card-title>
    <v-text-field
      label="Name"
      v-model="name"
    />
    <v-text-field
      label="Email"
      v-model="email"
    />
    <v-text-field
      label="Tel"
      v-model="tel"
    />
    <v-btn @click="addData"> ADD DATA </v-btn>
    </v-card>

  </v-dialog>
</template>

<script>
import axios from 'axios'
const url = "https://note-app0902.firebaseio.com/person/"
export default {
  name: 'Modal',
  data: function() {
    return {
      isDialogOpen: false,
      json_data: {},
      message: '',
      email: '',
      name: '',
      tel: '',
    }
  },
  methods: {
    addData() {
      if (this.email) {
        const add_url = url + this.email + '.json'
        const data = {
          'name': this.name,
          'tel': this.tel,
        }
        axios.put(add_url, data)
          .then( ( res ) => {
            this.email = ''
            this.name = ''
            this.tel = ''
          }).then(
            this.isDialogOpen = false
          )
      } else {
        confirm('cannot add empty data!')
      }
    },
  },
}
</script>