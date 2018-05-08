<template>
  <div class="col-sm-12">
    <ul class="pagination justify-content-center">
      <li class="page-item"><button class="border-primary rounded text-primary" :disabled="number == 1" @click="previousPage()">Previous</button></li>
      <li class="page-item"><button class="border-primary rounded text-primary" :disabled="number == pages || pages === 0" @click="nextPage()">Next</button></li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'paginator',
  props: ['pages', 'number', 'filterText'],
  data () {
    return {
      devices: [],
      paginatorNumber: 1,
      paginatorPages: 1
    }
  },
  methods: {
    previousPage () {
      this.paginatorNumber = this.number - 1
      const vm = this
      axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices?filter=' + vm.filterText + '&page=' + vm.paginatorNumber)
        .then((response) => {
          vm.devices = response.data.content
          vm.$emit('update', [vm.devices, vm.paginatorNumber])
        }, (error) => {
          console.log(error)
        })
    },
    nextPage () {
      this.paginatorNumber = this.number + 1
      const vm = this
      axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices?filter=' + vm.filterText + '&page=' + vm.paginatorNumber)
        .then((response) => {
          vm.devices = response.data.content
          vm.$emit('update', [vm.devices, vm.paginatorNumber])
        }, (error) => {
          console.log(error)
        })
    }
  }
}
</script>
<style lang="scss" scoped>
button{
cursor: pointer;
}

button:disabled,
button[disabled]{
  border: 1px solid #999999 !important;
  background-color: #cccccc !important;
  color: #666666 !important;
}
</style>
