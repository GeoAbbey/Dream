<template>
<v-container>
  <h2 class="mb-4" style="color: #757575">Guests</h2>
    <v-flex>
  <div>
    <v-dialog v-model="dialog" max-width="500px">
      <v-btn round slot="activator" color="primary" dark class="mb-2">Add Guest</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">{{ formTitle }}</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.firstName" label="First Name"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.lastName" label="Last Name"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.address" label="Address"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.email" label="Email"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.mobile" label="Mobile"></v-text-field>
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
        <td>{{ props.item.firstName }}</td>
        <td class="text-xs-center">{{ props.item.lastName }}</td>
        <td class="text-xs-center">{{ props.item.address }}</td>
        <td class="text-xs-center">{{ props.item.email }}</td>
        <td class="text-xs-center">{{ props.item.mobile }}</td>
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
          text: 'First Name',
          align: 'left',
          sortable: false,
          value: 'firstName'
        },
        { text: 'Last Name', align: 'center', value: 'lastName' },
        { text: 'Address', align: 'center', value: 'address' },
        { text: 'Email', align: 'center', value: 'email' },
        { text: 'Mobile', align: 'center', value: 'mobile' },
        { text: 'Actions', align: 'center', value: 'name', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        firstName: '',
        lastName: '',
        address: '',
        email: '',
        mobile: ''
      },
      defaultItem: {
        firstName: '',
        lastName: '',
        address: '',
        email: '',
        mobile: ''
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Add Guest' : 'Edit Guest'
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
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
          },
          {
            firstName: 'Ismail',
            lastName: 'Olasunkanmi',
            address: '14, Omotorisa Street, Idimu',
            email: 'olasunkanmiismail2@gmail.com',
            mobile: '+2347069359768'
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