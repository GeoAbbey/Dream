<template>
<v-container>
  <h2 class="mb-4" style="color: #757575">Media</h2>
  <v-layout row>
    <v-flex>
      <v-card>
        <v-flex pa-3>
        <v-subheader>April</v-subheader>
        </v-flex>
        <v-container fluid grid-list>
          <v-layout row wrap>
            <v-flex v-for="i in 6" :key="i" xs4>
              <img
                :src="`https://randomuser.me/api/portraits/men/${i + 20}.jpg`"
                class="image"
                alt="lorem"
                width="100%"
                height="100%"
              >
            </v-flex>
          </v-layout>
        </v-container>
        <v-flex pa-3>
        <v-subheader>May</v-subheader>
        </v-flex>
        <v-container fluid grid-list>
          <v-layout row wrap>
            <v-flex v-for="i in 6" :key="i" xs4>
              <img
                :src="`https://randomuser.me/api/portraits/women/${i + 5}.jpg`"
                class="image"
                alt="lorem"
                width="100%"
                height="100%"
              >
            </v-flex>
          </v-layout>
        </v-container>
        <v-footer class="mt-5"></v-footer>
      </v-card>
    </v-flex>
  </v-layout>
  </v-container>
</template>