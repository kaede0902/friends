<template>
  <v-dialog
    max-width="290"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-btn
        color="primary"
        dark
        v-bind="attrs"
        v-on="on"
      >
        Open Dialog
      </v-btn>
    </template>

    <v-card>
      <v-card-title class="text-h5">
        Friend Detail
      </v-card-title>
    </v-card>

  </v-dialog>
</template>

<script>
export default {
  name: 'Modal',
}
</script>