<template>
  <div class="container">
    <h1>Knetik Devices</h1>
    <hr>
    <p>Filter By:</p>
    <div class="form-group row">
      <label class="col-sm-2 col-form-label">Location:</label>
      <div class="col-sm-4">
        <input id="location-filter" name="location-filter" type="text" class="form-control" v-model="location"/>
      </div>
      <label class="col-sm-2 col-form-label">Parent Location:</label>
      <div class="col-sm-4">
        <input id="parent-filter" name="parent-filter" type="text" class="form-control" v-model="parentLocation"/>
      </div>
    </div>
    <div class="form-group row">
      <label class="col-sm-2 col-form-label">Connected:</label>
      <div class="col-sm-4">
        <select id="connected-filter" name="connected-filter" class="form-control" v-model="connected">
          <option selected > Choose an option...</option>
          <option value="true">True</option>
          <option value="false">False</option>
        </select>
      </div>
    </div>
    <div class="form-group">
    <button class="btn btn-success" @click="applyFilter()">Apply</button>
    </div>
    <hr>
    <paginator :number="number" :pages="pages" :filterText="filterText" @update="updateData"></paginator>
    <div>
      <device :device="device" v-for="device in devices" :key="device.id" ></device>
    </div>
    <paginator :number="number" :pages="pages" :filterText="filterText" @update="updateData"></paginator>
  </div>
</template>

<script>
import axios from 'axios'
import Device from './Device'
import Paginator from './Paginator'

export default {
  name: 'Home',
  data () {
    return {
      devices: [],
      location: '',
      connected: '',
      parentLocation: '',
      filterText: '',
      pages: 1,
      number: 1
    }
  },
  components: {
    Device,
    Paginator
  },
  created () {
    const vm = this
    axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices')
      .then((response) => {
        vm.devices = response.data.content
        vm.pages = response.data.total_pages
      }, (error) => {
        console.log(error)
      })
  },
  methods: {
    applyFilter () {
      const vm = this
      this.number = 1
      this.filterText = ''
      if (this.location !== '') {
        this.filterText += 'location:' + this.location + '%7C'
      }
      if (this.parentLocation !== '') {
        this.filterText += 'parent_location:' + this.parentLocation + '%7C'
      }
      if (this.connected !== '') {
        this.filterText += 'connected:' + this.connected + '%7C'
      }
      axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices?filter=' + vm.filterText)
        .then((response) => {
          vm.devices = response.data.content
          vm.pages = response.data.total_pages
        }, (error) => {
          console.log(error)
        })
    },
    updateData (data) {
      this.devices = data[0]
      this.number = data[1]
    }
  }
}
</script>

<style lang="scss">
.card{
  text-align: center;
}
</style>
