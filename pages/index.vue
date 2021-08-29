<template>
  <section>
    <h1>Friends {{ message }} </h1>
    <input v-model="email" />
    <br/>
    <input v-model="name" />
    <br/>
    <input v-model="tel" />
    <br/>
    <button @click="addData"> ADD DATA </button>
    <br/>
    <v-simple-table>
      <template v-slot:default>

        <thead>
          <tr>
            <th>
              email
            </th>
            <th>
              name
            </th>
            <th>
              tel
            </th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="(data, key) in json_data" :key="key"
          >
            <td>
              {{ key}}
            </td>
            <td>
              {{ data.name}}
            </td>
            <td>
              {{ data.tel}}
            </td>
          </tr>
        </tbody>

      </template>
    </v-simple-table>
  </section>
</template>

<script>
import axios from 'axios'
const url = "https://note-app0902.firebaseio.com/person/"

export default {
  data: function() {
    return {
      json_data: {},
      message: '',
      email: '',
      name: '',
      tel: '',
    }
  },
  created() {
    this.getData()
  },
  methods: {
    addData() {
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
          this.getData()
        })
    },
    getData() {
      axios.get(url + '.json')
        .then( (res) => {
          this.json_data = res.data
        }).catch((error) => {
          this.message = 'ERR'
          this.json_data = {}
      })
    },
  },
}
</script>