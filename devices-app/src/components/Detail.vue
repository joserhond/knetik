<template>
  <div class="container">
    <h1>{{device.id}}
      <span class="badge badge-secondary badge-success" v-if="device.connected==true">Connected</span>
      <span class="badge badge-secondary badge-danger" v-else> Offline</span>
    </h1>
    <ul class="list-group">
      <li class="list-group-item"><span class="label">Location: </span>{{device.location}}</li>
      <li class="list-group-item"><span class="label">MAC Address: </span>{{device.mac_address}}</li>
      <li class="list-group-item"><span class="label">Parent Location: </span>{{device.parent_location}}</li>
      <li class="list-group-item"><span class="label">Updated at: </span>{{device.updated_at}}</li>
      <li class="list-group-item"><span class="label">Signal Level: </span>
        <span class="badge badge-pill" v-bind:class="device.signal<0 ? 'badge-warning' : 'badge-primary'">{{device.signal}}</span></li>
    </ul>
    <router-link class="btn btn-secondary" :to="{ name: 'Home'}">Return to home</router-link>
    <h2>Related devices</h2>
    <paginator :number="number" :pages="pages" :filterText="filterText" @update="updateData"></paginator>
    <div class="related-container">
      <device :device="related" v-for="related in relatedDevices" :key="related.id" v-if="related.id!=device.id"></device>
    </div>
    <paginator :number="number" :pages="pages" :filterText="filterText" @update="updateData"></paginator>
  </div>
</template>

<script>
import axios from 'axios'
import Device from './Device'
import Paginator from './Paginator'

export default {
  name: 'Detail',
  data () {
    return {
      device: '',
      relatedDevices: [],
      id: this.$route.params.device_id,
      pages: 1,
      number: 1,
      filterText: ''
    }
  },
  components: {
    Device,
    Paginator
  },
  created () {
    const vm = this
    axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices?filter=id:' + this.id)
      .then((response) => {
        vm.device = response.data.content[0]
        axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices?filter=location:' + vm.device.location)
          .then((response) => {
            vm.relatedDevices = response.data.content
            vm.pages = response.data.total_pages
          }, (error) => {
            console.log(error)
          })
      }, (error) => {
        console.log(error)
      })
  },
  methods: {
    updateData (data) {
      this.relatedDevices = data[0]
      this.number = data[1]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.label{
  font-weight: 600;
}
.btn-secondary{
  margin:10px 0;
}

.badge-pill{
  font-size:100%;
}
</style>
