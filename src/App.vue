<template>
  <v-app>
    <v-toolbar>
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <!-- <router-view/> -->
      <v-dialog v-model="dialog" max-width="500px">
        <v-btn color="primary" dark slot="activator" class="mb-2">New Item</v-btn>
        <v-card>
          <v-card-title>
            <span class="headline">{{ formTitle }}</span>
          </v-card-title>
          <v-card-text>
            <v-container grid-list-md>
              <v-layout wrap>
                <v-flex xs12 sm6 md4>
                  <v-text-field label="Employer" v-model="editedItem.name"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-select
                    v-bind:items="states"
                    v-model="editedItem.state"
                    label="State"
                    single-line
                  ></v-select>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field label="Category" v-model="editedItem.category"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field label="Score" v-model="editedItem.score"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field label="Test" v-model="editedItem.test"></v-text-field>
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
      <!-- toggle hide-actions for pagination -->
      <v-data-table
        :headers="headers"
        :items="items"
        hide-actions
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td>{{ props.item.name }}</td>
          <td>
            <!-- Added v-model to bind to object property -->
              <v-select
                v-bind:items="states"
                v-model="props.item.state"
                label="State"
                single-line
              ></v-select>
          </td>
          <td>
            <v-menu
              lazy
              :close-on-content-click="true"
              transition="scale-transition"
              offset-y
              full-width
              :nudge-right="40"
              max-width="290px"
              min-width="290px">
              <v-text-field
                slot="activator"
                label="Start Date"
                v-model="props.item.date"
                prepend-icon="event"
                required
              ></v-text-field>
              <v-date-picker
                type="date"
                v-model="props.item.date"
                no-title
                scrollable
                show-current
              >
              </v-date-picker>
            </v-menu>
          </td>
          <td class="">{{ props.item.category }}</td>
          <td class="">{{ props.item.score }}</td>
          <td class="">{{ props.item.test }}</td>
          <td>
            <v-text-field
              name="input-2"
              label="Label Text"
              v-model="props.item.TextValue"
            ></v-text-field>
          </td>
          <td class="justify-center layout px-0">
            <v-btn icon class="mx-0" @click="editItem(props.item)">
              <v-icon color="teal">edit</v-icon>
            </v-btn>
            <v-btn icon class="mx-0" @click="deleteItem(props.item)">
              <v-icon color="pink">delete</v-icon>
            </v-btn>
          </td>
        </template>
      </v-data-table>
    </v-content>
  </v-app>
</template>

<script>
/* eslint-disable */
export default {
  computed: {
    formTitle () {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
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
      this.items = [
{
          name: 'Samsung',
          state: null,
          category: 159,
          score: 6.0,
          test: 24,
          date: null,
          TextValue: null
        },
        {
          name: 'Panasonic',
          state: null,
          category: 237,
          score: 9.0,
          test: 37,
          date: null,
          TextValue: null
        },
        {
          name: 'Sony',
          state: null,
          category: 262,
          score: 16.0,
          test: 23,
          date: null,
          TextValue: null
        },
        {
          name: 'Toshiba',
          state: null,
          category: 305,
          score: 3.7,
          test: 67,
          date: null,
          TextValue: null
        },
        {
          name: 'LG',
          state: null,
          category: 356,
          score: 16.0,
          test: 49,
          date: null,
          TextValue: null
        },
        {
          name: 'JVC',
          state: null,
          category: 375,
          score: 0.0,
          test: 94,
          date: null,
          TextValue: null
        },
        {
          name: 'Lenovo',
          state: null,
          category: 392,
          score: 0.2,
          test: 98,
          date: null,
          TextValue: null
        },
        {
          name: 'Hewlett Packard',
          state: null,
          category: 408,
          score: 3.2,
          test: 87,
          date: null,
          TextValue: null
        },
        {
          name: 'Hitachi',
          state: null,
          category: 452,
          score: 25.0,
          test: 51,
          date: null,
          TextValue: null
        },
        {
          name: 'Logitec',
          state: null,
          category: 518,
          score: 26.0,
          test: 65,
          date: null,
          TextValue: null
        }
      ]
    },
    editItem (item) {
      this.editedIndex = this.items.indexOf(item)
      this.editedItem = Object.assign({}, item)
      this.dialog = true
    },
    deleteItem (item) {
      const index = this.items.indexOf(item)
      confirm('Are you sure you want to delete this item?') && this.items.splice(index, 1)
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
        Object.assign(this.items[this.editedIndex], this.editedItem)
      } else {
        this.items.push(this.editedItem)
      }
      this.close()
    }
  },
  data () {
    return {
      title: "Singular Vue",
      menu: false,
      items: [],
      editedIndex: -1,
      editedItem: {
        name: '',
          state: null,
          category: 0,
          score: 0,
          test: 0,
          date: null,
          TextValue: null
      },
      defaultItem: {
        name: '',
          state: null,
          category: 0,
          score: 0,
          test: 0,
          date: null,
          TextValue: null
      },
      states: [
          { text: 'State 1', value:1, group : 'Group 1'},
          { text: 'State 2', value:2, group : 'Group 2'},
          { text: 'State 3', value:3, group : 'Group 3'},
          { text: 'State 4', value:4, group : 'Group 4'},
          { text: 'State 5', value:5, group : 'Group 5'},
          { text: 'State 6', value:6, group : 'Group 6'},
          { text: 'State 7', value:7, group : 'Group 7'}
        ],
      headers: [
        { text: "Employer", align: "left", sortable: false, value: "name"},
        { text: "State", value: "state", sortable: null},
        { text: "Date", value: "date", width: '20%' },
        { text: "Category", value: "category" },
        { text: "Score", value: "score" },
        { text: "Test", value: "test" },
        { text: "TextValue", value: "Some Text" }
      ]
    };
  },
  name: "App"
};
</script>
