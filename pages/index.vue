<template>
  <v-container>
    <v-row>
      <v-data-table
        :headers="headers"
        :items="items"
      >
        <template v-slot:item.src="{ item }">
          <img
            :src="item.src"
            style="width: 100px; height: 100px"
            @click="openURL(item)"
          >
        </template>
        <template v-slot:item.yield="{ item }">
          {{ (item.monthly * 12) / ( item.price * 0.11) * 100 }}
        </template>
      </v-data-table>
    </v-row>
    <v-row>
      <v-btn block color="success" @click="load">
        text
      </v-btn>
    </v-row>
  </v-container>
</template>

<script>

export default {

  data () {
    return {
      items: [],
      headers: [
        {
          text: '',
          value: 'src'
        },
        {
          text: 'price',
          value: 'price'
        },
        {
          text: 'provision',
          value: 'provision'
        },
        {
          text: 'size',
          value: 'size'
        },
        {
          text: 'yield',
          value: 'yield'
        }
      ]
    }
  },

  methods: {
    async load ({ $api }) {
      const { data } = await this.$api.Data.get()
      this.items = data
    },

    openURL (item) {
      window.open(item.url)
    }
  }
}
</script>
