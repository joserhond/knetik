<template>
  <div class="col-lg-4 col-md-6 card-container">
    <div class="card bg-light">
      <div class="card-body">
        <h6 class="card-title">{{device.id}}</h6>
        <p class="card-text">
          <span class="badge badge-success" v-if="device.connected==true">Connected</span>
          <span class="badge badge-danger" v-else> Offline</span>
          - Location: {{device.location}}
        </p>
        <router-link class="btn btn-info" :to="{ name: 'Detail', params: { device_id: device.id }}">View Details</router-link>
      </div>
      <div class="card-footer">
        <small class="text-muted">Updated at: {{device.updated_at}}</small>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'device',
  props: ['device']
}
</script>

<style land="scss" scoped>
.card-container{
  display: inline-block;
  margin-bottom:10px;
  padding-right: 0;
  padding-left:0;
}

@media(min-width: 768px){
  .card-container:nth-child(2n){
    padding-right: 0;
    padding-left: 7.5px;
  }
  .card-container:nth-child(2n+1){
    padding-left: 0;
    padding-right: 7.5px;
  }
}

@media(min-width: 991px){
  .card-container:nth-child(3n){
    padding-right: 0;
    padding-left: 7.5px;
  }
  .card-container:nth-child(3n+1){
    padding-left: 0;
    padding-right: 7.5px;
  }
  .card-container:nth-child(3n+2){
    padding-left: 7.5px;
    padding-right: 7.5px;
  }
}

</style>
