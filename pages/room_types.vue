<template>
<v-container mt-0>
  <h2 class="mb-4" style="color: #757575">Room Types</h2>
    <v-flex>
  <div>
    <v-dialog v-model="dialog" max-width="500px">
      <v-btn round slot="activator" color="primary" dark class="mb-2">Add Room Type</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">{{ formTitle }}</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.serialNumber" label="S/N"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.name" label="Name"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.shortCode" label="Short Code"></v-text-field>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click.native="close">Cancel</v-btn>
          <v-btn color="blue darken-1" flat @click.native="save">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-data-table
      :headers="headers"
      :items="desserts"
      hide-actions
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td class="text-xs-center">{{ props.item.serialNumber }}</td>
        <td class="text-xs-left">{{ props.item.name }}</td>
        <td class="text-xs-center">{{ props.item.shortCode }}</td>
        <td class="justify-center layout px-0">
          <v-btn icon class="mx-0" @click="editItem(props.item)">
            <v-icon color="teal">edit</v-icon>
          </v-btn>
          <v-btn icon class="mx-0" @click="deleteItem(props.item)">
            <v-icon color="pink">delete</v-icon>
          </v-btn>
        </td>
      </template>
      <template slot="no-data">
        <v-btn color="primary" @click="initialize">Reset</v-btn>
      </template>
    </v-data-table>
  </div>
  </v-flex>
</v-container>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      headers: [
        {
          text: 'S/N',
          align: 'center',
          value: 'serialNumber'
        },
        { text: 'Name', align: 'left', value: 'name' },
        { text: 'Short Code', align: 'center', value: 'shortCode' },
        { text: 'Actions', align: 'center', value: 'name', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        serialNumber: 0,
        name: '',
        shortCode: ''
      },
      defaultItem: {
        serialNumber: 0,
        name: '',
        shortCode: ''
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Add Room Type' : 'Edit Room Type'
      }
    },

    watch: {
      dialog (val) {
        val || this.close()
      }
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.desserts = [
          {
            serialNumber: 1,
            name: 'Grand Swiss Cottage',
            shortCode: 'GSC'
          },
          {
            serialNumber: 2,
            name: 'Super Delux',
            shortCode: 'SD'
          },
          {
            serialNumber: 3,
            name: 'Honeymoon Suite',
            shortCode: 'HS'
          },
          {
            serialNumber: 4,
            name: 'Delux Room',
            shortCode: 'DR'
          }
        ]
      },

      editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },

      deleteItem (item) {
        const index = this.desserts.indexOf(item)
        confirm('Are you sure you want to delete this item?') && this.desserts.splice(index, 1)
      },

      close () {
        this.dialog = false
        setTimeout(() => {
          this.editedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        }, 300)
      },

      save () {
        if (this.editedIndex > -1) {
          Object.assign(this.desserts[this.editedIndex], this.editedItem)
        } else {
          this.desserts.push(this.editedItem)
        }
        this.close()
      }
    }
  }
</script>