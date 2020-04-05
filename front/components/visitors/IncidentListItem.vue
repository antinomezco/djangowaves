<template>
  <div>
    <h2>{{ incident.title }}</h2>
    <p>{{ lastUpdate.description }}</p>
    <div class="sub">
      {{ lastUpdate.date | timeAgo }}
      <span class="right">
        Status: {{ lastUpdate.status }}
      </span>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'Incident',
  // data: () => ({
  //   openIncidents: [{ id: 1, title: 'Connectivity Issues', update_set: [{ description: 'We have noticed some connectivity issues', date: '2019-10-02 13:00:12', status: 'Investigating' }] }]
  // }),
  filters: {
    timeAgo (value) {
      return moment.utc(value).fromNow()
    }
  },
  props: {
    incident: {
      type: Object,
      default: () => { return {} }
    }
  },
  computed: {
    lastUpdate () {
      return this.incident.update_set[0]
    }
  }
}
</script>

<style scoped>
  .sub {
    color: #999999;
  }
  .right {
    float: right;
  }
  h2 {
    margin-bottom: 10px;
  }
</style>
