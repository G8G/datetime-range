<template>
  <q-layout>
    <div class="width-1of5 item-filter">
      <h3>Data:</h3>
      <div v-for="(column, index) in tableColumns" :key="index">
        <!-- Datetime Range -->
        <q-datetime-range
          type="date"
          v-model="column.model.range"
          :format="column.model.format"
        />
      </div>
      <q-datetime-range
        type="date"
        v-model="range"
        :format="format"
      />
    </div>
  </q-layout>
</template>

<script>
import _ from 'Lodash'
import moment from 'moment'

export default {
  data () {
    return {
      tableColumns: undefined,
      columns: [
        {
          title: 'Data',
          id: 'date'
        }
      ],
      format: moment.localeData().longDateFormat('L'),
      range: {
        from: '',
        to: ''
      }
    }
  },
  mounted () {
    this.modifyColumns()
  },
  methods: {
    modifyColumns () {
      // Add a model propertie to all parameter
      this.tableColumns = _.map(this.columns, o => {
        return _.extend({ model: {
          format: moment.localeData().longDateFormat('L'),
          range: {
            from: '',
            to: ''
          }
        }}, o)
      })
    }
  }
}
</script>

<style lang="stylus">
.textfield
    background #AAA
    color #2020A5
</style>
