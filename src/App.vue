<template>
  <v-app>
    <v-toolbar
      app
      :clipped-left="clipped"
    >
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
          <td class="text-xs-right">{{ props.item.username }}</td>
          <td class="text-xs-right">{{ props.item.email }}</td>
          <td class="text-xs-right">{{ props.item.phone }}</td>
          <td class="text-xs-right">{{ props.item.website }}</td>
          <td class="text-xs-right">{{ props.item.company.name }}</td>
        </template>
      </v-data-table>
    </v-content>
    <!-- <v-footer :fixed="fixed" app>
      <span>&copy; Just a demo, 2018</span>
    </v-footer> -->
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      right: true,
      title: "Singular Vue",
      headers: [
        {
          text: "Dessert (100g serving)",
          align: "left",
          sortable: false,
          value: "name"
        },
        { text: "Calories", value: "calories" },
        { text: "Fat (g)", value: "fat" },
        { text: "Carbs (g)", value: "carbs" },
        { text: "Protein (g)", value: "protein" },
        { text: "Iron (%)", value: "iron" }
      ],
      items: [],
      methods: {
        getData: function(){
            var root = 'https://jsonplaceholder.typicode.com';
                          var vm = this;
                          $.ajax({
                              url: root + '/users',#
                              method: 'GET'
                          }).then(function (data) {
                              vm.items = data;
                          });                             

        }
      },
      ready: this.items = this.getData()
    };
  },
  name: "App"
};
</script>
