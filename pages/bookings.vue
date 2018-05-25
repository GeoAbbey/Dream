<template>
<v-container>
  <h2 class="mb-4" style="color: #757575">Bookings</h2>
    <v-flex>
  <div>
    <v-dialog v-model="dialog" max-width="500px">
      <v-btn round slot="activator" color="primary" dark class="mb-2">Add Booking</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">{{ formTitle }}</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.room" label="Room"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.checkIn" label="Check in"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.checkOut" label="Check out"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.paymentStatus" label="Payment Status"></v-text-field>
              </v-flex>
              <v-flex xs12 sm6 md4>
                <v-text-field v-model="editedItem.bookingStatus" label="Booking Status"></v-text-field>
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
        <td>{{ props.item.room }}</td>
        <td class="text-xs-center">{{ props.item.checkIn }}</td>
        <td class="text-xs-center">{{ props.item.checkOut }}</td>
        <td class="text-xs-center">{{ props.item.paymentStatus }}</td>
        <td class="text-xs-center">{{ props.item.bookingStatus }}</td>
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
          text: 'Room',
          align: 'left',
          sortable: false,
          value: 'room'
        },
        { text: 'Check in', align: 'center', value: 'checkIn' },
        { text: 'Check out', align: 'center', value: 'checkOut' },
        { text: 'Payment Status', align: 'center', value: 'paymentStatus' },
        { text: 'Booking Status', align: 'center', value: 'bookingStatus' },
        { text: 'Actions', align: 'center', value: 'room', sortable: false }
      ],
      desserts: [],
      editedIndex: -1,
      editedItem: {
        room: '',
        checkIn: '',
        checkOut: '',
        paymentStatus: '',
        bookingStatus: ''
      },
      defaultItem: {
        room: '',
        checkIn: '',
        checkOut: '',
        paymentStatus: '',
        bookingStatus: ''
      }
    }),

    computed: {
      formTitle () {
        return this.editedIndex === -1 ? 'Add Booking' : 'Edit Booking'
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
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
          },
          {
            room: 'Kings Court',
            checkIn: '24/05/2018',
            checkOut: '26/05/2018',
            paymentStatus: 'Paid',
            bookingStatus: 'Completed'
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