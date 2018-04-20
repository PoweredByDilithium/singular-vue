<template>
  <v-app>
    <v-toolbar>
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <!-- <router-view/> -->
      <v-data-table
        :headers="headers"
        :items="items"
        hide-actions
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td>{{ props.item.name }}</td>
          <td>
              <v-select
                :items="states"
                label="Status"
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
              min-width="290px"
              :return-value.sync="props.item.date">
              <v-text-field
                slot="activator"
                label="Start Date"
                v-model="props.item.date"
                prepend-icon="event"
                required
                readonly
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
        </template>
      </v-data-table>
    </v-content>
  </v-app>
</template>

<script>
/* eslint-disable */
export default {
  data () {
    return {
      title: "Singular Vue",
      menu: false,
      states: [
          { text: 'State 1', number: 2 },
          { text: 'State 2' },
          { text: 'State 3' },
          { text: 'State 4' },
          { text: 'State 5' },
          { text: 'State 6' },
          { text: 'State 7' }
        ],
      headers: [
        { text: "Employer", align: "left", sortable: false, value: "name"},
        { text: "Category", value: "category" },
        { text: "Date", value: "date", width: '20%' },
        { text: "Performance", value: "performance" },
        { text: "Score", value: "score" },
        { text: "Test", value: "test" }
      ],  
      items: [{
          name: 'Samsung',
          category: 159,
          score: 6.0,
          test: 24,
          date: null
        },
        {
          name: 'Panasonic',
          category: 237,
          score: 9.0,
          test: 37,
          date: null
        },
        {
          name: 'Sony',
          category: 262,
          score: 16.0,
          test: 23,
          date: null
        },
        {
          name: 'Toshiba',
          category: 305,
          score: 3.7,
          test: 67,
          date: null
        },
        {
          name: 'LG',
          category: 356,
          score: 16.0,
          test: 49,
          date: null
        },
        {
          name: 'JVC',
          category: 375,
          score: 0.0,
          test: 94,
          date: null
        },
        {
          name: 'Lenovo',
          category: 392,
          score: 0.2,
          test: 98,
          date: null
        },
        {
          name: 'Hewlett Packard',
          category: 408,
          score: 3.2,
          test: 87,
          date: null
        },
        {
          name: 'Hitachi',
          category: 452,
          score: 25.0,
          test: 51,
          date: null
        },
        {
          name: 'Logitec',
          category: 518,
          score: 26.0,
          test: 65,
          date: null
        }]
    };
  },
  name: "App"
};
</script>
