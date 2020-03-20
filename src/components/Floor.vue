<template>
  <v-col>
    <v-row style="height: 3em">
      <v-card v-for="cube in cubes" v-bind:key="cube.id" class="pa-1 ma-1 elevation-2" color="#ddd" width="7em" height="7em">
        <span
          class="caption text-no-wrap"
          style="background: #bbb; display: block; text-align: center"
        >{{cube.id}}</span>
        <div style="text-align: center; margin-top: 0.5em">
          <v-avatar :color="!cube.occupant.name ? '#ccc' : 'orange'" size="36" class="mr-1">
            <v-icon dark>mdi-account-circle</v-icon>
          </v-avatar>
          <br />
          <span class="caption" style="display: inline-block">{{cube.occupant.name}}</span>
        </div>
      </v-card>
    </v-row>
  </v-col>
</template>

<script>
import axios from 'axios';

export default {
  components: {},
  props: {
    floor: String
  },
  data: () => ({
    // TODO: Get floors data from API
    floors: [{"id":"Seating 5th","size":{"height":11,"width":30}},{"id":"Seating 3rd","size":{"height":11,"width":30}}],
    cubes: [],
    isLoading: false,
    model: null,
    search: null,
  }),
  mounted() {
    // TODO: How do we know what floor we're displaying? We prolly need to use Vue routing and URI's to represent what floor we're showing (something like ?floor=E5)
    // TODO: Filter out cubes that aren't on the floor we're showing
    // TODO: Respect the size of cube
    // TOOD: Respect the length of the floor. Rows should fill until we have hit the max, then start a new row
    // TODO: Pull in rooms and populate the middle of the floor with the conference/office rooms
    // TODO: Figure out how to stretch the background image when the floor overflows
    // TODO: Order cubes and rooms into a sequenced array that respects their x/y coordinates
    this.cubes = axios.get("/cubicles").then(response => { this.cubes = response.data});
  }
};
</script>