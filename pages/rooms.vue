<template>
<v-container mt-0>
    <h2 class="mb-4" style="color: #757575">Rooms</h2>
    <v-flex>
  <div>
    <v-dialog v-model="dialog" max-width="500px">
      <v-btn round slot="activator" color="primary" dark class="mb-2">Add Room</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">{{ formTitle }}</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.roomNumber" label="Room Number"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.roomType" label="Room Type"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.floorNumber" label="Floor Number"></v-text-field>
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
        <td class="text-xs-center">{{ props.item.roomNumber }}</td>
        <td class="text-xs-left">{{ props.item.roomType }}</td>
        <td class="text-xs-left">{{ props.item.floorNumber }}</td>
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
          text: 'Room Number',
          align: 'center',
          value: 'roomNumber'
        },
        { text: 'Room Type', align: 'left', value: 'roomType' },
        { text: 'Floor Number', align: 'left', value: 'floorNumber' },
        { text: 'Actions', align: 'center', value: 'roomNumber', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        roomNumber: 0,
        roomType: '',
        floorNumber: ''
      },
      defaultItem: {
        roomNumber: 0,
        roomType: '',
        floorNumber: ''
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Add Room' : 'Edit Room'
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
            roomNumber: 1,
            roomType: 'Grand Swiss Cottage',
            floorNumber: 'F1-First Floor'
          },
          {
            roomNumber: 2,
            roomType: 'Super Delux',
            floorNumber: 'F2-Second Floor'
          },
          {
            roomNumber: 3,
            roomType: 'Honeymoon Suite',
            floorNumber: 'F3-Third Floor'
          },
          {
            roomNumber: 4,
            roomType: 'Delux Room',
            floorNumber: 'F4-Fourth Floor'
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