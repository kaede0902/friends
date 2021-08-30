<template>
  <v-app>
    <h1>Friends {{ message }} </h1>
    <Modal />
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
  </v-app>
</template>

<script>
import axios from 'axios'
import Modal from '../components/Modal'
const url = "https://note-app0902.firebaseio.com/person/"

export default {
  name: 'index',
  components: {
    Modal,
  },
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