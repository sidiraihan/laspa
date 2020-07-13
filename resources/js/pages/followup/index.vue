<template>
  <card :title="$t('Follow up')">
              <router-link :to="{ name: 'followup.create' }" class="btn btn-primary mb-3" active-class="active">
                {{ $t('Add') }}
              </router-link>
  
    <data-table
        :data="data"
        :columns="columns"
        @onTablePropsChanged="reloadTable">
    </data-table>
  </card>



</template>

<script>
import Form from 'vform'
import axios from 'axios'

// import { mapGetters } from 'vuex'

export default {
  scrollToTop: false,

  metaInfo () {
    return { title: this.$t('Follow Up') }
  },

   data() {
        return {
            url: "api/crm/listajax",
            data: {},
            tableProps: {
                search: '',
                length: 10,
                column: 'id',
                dir: 'asc'
            },
            columns: [
                {
                    label: 'ID',
                    name: 'id',
                    orderable: true,
                },
                {
                    label: 'Name',
                    name: 'name',
                    orderable: true,
                },
                {
                    label: 'Email',
                    name: 'email',
                    orderable: true,
                },
                {
                    label: 'Phone',
                    name: 'phone',
                    orderable: true,
                },
            ]
        }
    },

  // computed: mapGetters({
  //   data: 'auth/crm/listajax'
  // }),

  created () {
    this.getData(this.url);
  },

  methods: {
     getData(url = this.url, options = this.tableProps) {
            axios.get(url, {
                params: options
            })
            .then(response => {
                this.data = response.data;
            })
            // eslint-disable-next-line
            .catch(errors => {
                console.log(errors);
            })
        },
        reloadTable(tableProps) {
            this.getData(this.url, tableProps);
        }
  }
}
</script>
