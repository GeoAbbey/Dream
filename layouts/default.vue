<template>
  <v-app id="inspire">
    <v-navigation-drawer
      :clipped="$vuetify.breakpoint.lgAndUp"
      v-model="drawer"
      fixed
      app
    >
      <v-list dense>
        <template v-for="item in items">
          <v-layout
            v-if="item.heading"
            :key="item.heading"
            row
            align-center
          >
            <v-flex xs6>
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
            </v-flex>
            <v-flex xs6 class="text-xs-center">
              <a href="#!" class="body-2 black--text">EDIT</a>
            </v-flex>
          </v-layout>
          <v-list-group
            v-else-if="item.children"
            v-model="item.model"
            :key="item.text"
            :prepend-icon="item.model ? item.icon : item['icon-alt']"
            append-icon=""
          >
            <v-list-tile slot="activator">
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ item.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
            <v-list-tile
              v-for="(child, i) in item.children"
              :key="i"
              :to="child.to"
            >
              <v-list-tile-action v-if="child.icon">
                <v-icon>{{ child.icon }}</v-icon>
              </v-list-tile-action>
              <v-list-tile-content>
                <v-list-tile-title>
                  {{ child.text }}
                </v-list-tile-title>
              </v-list-tile-content>
            </v-list-tile>
          </v-list-group>
          <v-list-tile v-else :key="item.text" :to="item.to">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      color="blue darken-3"
      dark
      app
      fixed
    >
      <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
        <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
        <span class="hidden-sm-and-down">World Palace Hotel</span>
      </v-toolbar-title>
      <v-layout justify-center>
      <v-badge left color="red">
        <span slot="badge">8</span>
        <v-icon medium>notifications</v-icon>
      </v-badge>
      <v-badge color="red">
        <span slot="badge">5</span>
      <v-icon medium>mail</v-icon>
      </v-badge>
      </v-layout>
    </v-toolbar>
    <v-content>
      <v-container fluid fill-height>
        <v-layout justify-center align-center>
          <nuxt />
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      drawer: null,
      items: [
        { icon: 'dashboard', text: 'Dashboard', to: '/' },
        { icon: 'book', text: 'Bookings', to: '/bookings' },
        { icon: 'group', text: 'Guests', to: '/guests' },
        { icon: 'event', text: 'Availability Calendar', to: '/calendar' },
        { icon: 'perm_media', text: 'Media', to: '/media' },
        { icon: 'fastfood', text: 'Recipe Formulas', to: '/recipe' },
        {
          icon: 'keyboard_arrow_up',
          'icon-alt': 'keyboard_arrow_down',
          text: 'Hotel Configuration',
          model: false,
          children: [
            { icon: 'radio_button_unchecked', text: 'Room Types', to: '/room_types' },
            { icon: 'radio_button_unchecked', text: 'Rooms', to: '/rooms' },
            { icon: 'radio_button_unchecked', text: 'Price Manager' },
            { icon: 'radio_button_unchecked', text: 'Paid Services' },
            { icon: 'radio_button_unchecked', text: 'Coupon Management' },
            { icon: 'radio_button_unchecked', text: 'Floors' },
            { icon: 'radio_button_unchecked', text: 'Amenities' }
          ]
        },
        {
          icon: 'keyboard_arrow_up',
          'icon-alt': 'keyboard_arrow_down',
          text: 'Reports',
          model: false,
          children: [
            { icon: 'radio_button_unchecked', text: 'Occupancy' },
            { icon: 'radio_button_unchecked', text: 'Guest' },
            { icon: 'radio_button_unchecked', text: 'Financial' },
            { icon: 'radio_button_unchecked', text: 'Coupon' },
            { icon: 'radio_button_unchecked', text: 'Expenses' }
          ]
        },
        {
          icon: 'keyboard_arrow_up',
          'icon-alt': 'keyboard_arrow_down',
          text: 'HR Management',
          model: false,
          children: [
            { icon: 'radio_button_unchecked', text: 'Employees' },
            { icon: 'radio_button_unchecked', text: 'Departments' },
            { icon: 'radio_button_unchecked', text: 'Designations' }
          ]
        },
        {
          icon: 'keyboard_arrow_up',
          'icon-alt': 'keyboard_arrow_down',
          text: 'Expenses',
          model: false,
          children: [
            { icon: 'radio_button_unchecked', text: 'Expenses' },
            { icon: 'radio_button_unchecked', text: 'Expenses Category' }
          ]
        }
      ]
    }),
    props: {
      source: String
    }
  }
</script>
