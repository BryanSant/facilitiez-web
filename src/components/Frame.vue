<template>
  <v-app id="inspire">      
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
      dark
    >
      <v-list dense>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-view-dashboard</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Floors</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider class="mx-4" :inset="inset" horizontal></v-divider>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-home-account</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Rooms</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-account-multiple</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Teams</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-account</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>People</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-divider class="mx-4" :inset="inset" horizontal></v-divider>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-cog</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      clipped-left
      color="#7fbe41"
      dark
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <img width="70em" src="https://intranet.mychg.com/Assets/Uploaded-Photos/4b8973cc-8abd-477e-b6b7-36dcfc07464a.png"/><v-toolbar-title>Facilities</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-autocomplete
        v-model="model"
        :items="items"
        :loading="isLoading"
        :search-input.sync="search"
        hide-details
        hide-selected
        item-text="name"
        item-value="value"
        prepend-icon="mdi-magnify"
        label="Search for a rooms, teams, cubes, or people ..."
        rounded
      >        
      </v-autocomplete>
    </v-app-bar>

    <v-img style="position: absolute; width: 100%; height: 100%" src="@/assets/chg-headquarters-b.jpg"></v-img>
    <v-content>
      <Floor/>
    </v-content>

    <v-footer app>
      <span>&copy; 2020</span>
    </v-footer>
  </v-app>
</template>

<script>
  import Floor from './Floor';

  export default {
    components: {
      Floor,
    },
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      entries: [],
      isLoading: false,
      model: null,
      search: null,
    }),
    created () {
      this.$vuetify.theme.false = false
    },
    computed: {
      fields () {
        if (!this.model) return []

        return Object.keys(this.model).map(key => {
          return {
            key,
            value: this.model[key] || 'n/a',
          }
        })
      },
      items () {
        return this.entries.map(entry => {
          const Description = entry.Description.length > this.descriptionLimit
            ? entry.Description.slice(0, this.descriptionLimit) + '...'
            : entry.Description

          return Object.assign({}, entry, { Description })
        })
      },
    },
    watch: {
      /*
      search (val) {
        // Items have already been loaded
        if (this.items.length > 0) return

        // Items have already been requested
        if (this.isLoading) return

        this.isLoading = true

        // Lazily load input items
        fetch('https://api.publicapis.org/entries')
          .then(res => res.json())
          .then(res => {
            const { count, entries } = res
            this.count = count
            this.entries = entries
          })
          .catch(err => {
            console.log(err)
          })
          .finally(() => (this.isLoading = false))
      },
      */
    },
  }
</script>
