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
        <v-menu>
          <v-text-field
            slot="activator"
            label="Start Date"
            v-model="date"
            prepend-icon="event"
            readonly
          ></v-text-field>
          <v-date-picker
            type="month"
            v-model="date"
            no-title
            scrollable
          >
          </v-date-picker>
        </v-menu>
          </td>
          <td class="text-xs-right">{{ props.item.category }}</td>
          <td class="text-xs-right">{{ props.item.score }}</td>
          <td class="text-xs-right">{{ props.item.test }}</td>
        </template>
      </v-data-table>
    </v-content>
    <!-- <v-footer :fixed="fixed" app>
      <span>&copy; Just a demo, 2018</span>
    </v-footer> -->
  </v-app>
</template>

<script>
/* eslint-disable */
export default {
  data () {
    return {
      title: "Singular Vue",
      date: null,
      menu: false,
      modal: false,
      states: [
          { text: 'State 1' },
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
        { text: "Date", value: "date" },
        { text: "Performance", value: "performance" },
        { text: "Score", value: "score" },
        { text: "Test", value: "test" }
      ],
      items: [{
          value: false,
          name: 'Frozen Yogurt',
          category: 159,
          score: 6.0,
          test: 24,
          protein: 4.0,
          iron: '1%'
        },
        {
          value: false,
          name: 'Ice cream sandwich',
          category: 237,
          score: 9.0,
          test: 37,
          protein: 4.3,
          iron: '1%'
        },
        {
          value: false,
          name: 'Eclair',
          category: 262,
          score: 16.0,
          test: 23,
          protein: 6.0,
          iron: '7%'
        },
        {
          value: false,
          name: 'Cupcake',
          category: 305,
          score: 3.7,
          test: 67,
          protein: 4.3,
          iron: '8%'
        },
        {
          value: false,
          name: 'Gingerbread',
          category: 356,
          score: 16.0,
          test: 49,
          protein: 3.9,
          iron: '16%'
        },
        {
          value: false,
          name: 'Jelly bean',
          category: 375,
          score: 0.0,
          test: 94,
          protein: 0.0,
          iron: '0%'
        },
        {
          value: false,
          name: 'Lollipop',
          category: 392,
          score: 0.2,
          test: 98,
          protein: 0,
          iron: '2%'
        },
        {
          value: false,
          name: 'Honeycomb',
          category: 408,
          score: 3.2,
          test: 87,
          protein: 6.5,
          iron: '45%'
        },
        {
          value: false,
          name: 'Donut',
          category: 452,
          score: 25.0,
          test: 51,
          protein: 4.9,
          iron: '22%'
        },
        {
          value: false,
          name: 'KitKat',
          category: 518,
          score: 26.0,
          test: 65,
          protein: 7,
          iron: '6%'
        }]
    };
  },
  name: "App"
};
</script>
