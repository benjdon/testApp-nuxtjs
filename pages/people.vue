<template>
  <v-card outlined width="80%" class="mx-auto rounded-0 pa-10">
    <v-card-text>
      <v-data-table
        :headers="headers"
        :items="items"
        :items-per-page="perPage"
        :page.sync="page"
        :loading="loading"
        @page-count="pageCount = $event"
        class="elevation-0"
        hide-default-footer
      >
      </v-data-table>
      <div class="pt-2 d-flex justify-end">
        <v-pagination
          v-model="page"
          :length="pageCount"
        ></v-pagination>
      </div>
    </v-card-text>
  </v-card>
</template>

<script lang="ts">
  import { Vue, Component } from 'vue-property-decorator'
  
  @Component({})
  export default class People extends Vue {
    loading: boolean = true
    items: any = [];
    page: number = 1;
    perPage: number = 10;
    perPageOptions: any = [10, 20, 50, 100];
    pageCount: any = 0;
    headers = [
      { text: "ID", value: "id" },
      { text: "First Name", value: "first_name" },
      { text: "Last Name", value: "last_name" },
      { text: "Street", value: "street" },
      { text: "City", value: "city" },
      { text: "Zipcode", value: "zipcode" },
      { text: "Actions", value: "actions", sortable: false },
    ];

    mounted() {
      this.query();
    }
  
    async query() {
      this.loading = true;
      try {
        const { data: data } = await this.$axios.get('/api/test');
        if(data.count > 0) {
          this.items = data.results;
          this.pageCount = Math.ceil(data.count / this.perPage);
        }
      } catch (error) {
        
      }
      this.loading = false;
    }
  }
</script>
