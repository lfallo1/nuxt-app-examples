<template>
  <section class="container">
    <div>
      <h1 class="title">
        VP Reports UI
      </h1>
      <div class="row">
        <div class="align-center col-xs-12">
          <b-btn v-if="!refreshing" variant="outline-success" @click="refreshPrograms()">Refresh Programs</b-btn>
          <b-btn v-else :disabled="true" variant="outline-success">Refreshing Programs</b-btn>
        </div>
      </div>
      <nuxt-link to="/about">About</nuxt-link>
    </div>

  </section>
</template>

<script>

  import axios from 'axios';
  import Vue from 'vue';

export default {
  data(){
    return {
      refreshing: false
    }
  },
  methods:{
    refreshPrograms(){
      this.refreshing = true;
      axios.get('http://localhost:8080/api/report')
        .then(() =>{
          this.refreshing = false;
          Vue.toasted.success('Program Information Refreshed', {
            position: 'bottom-right',
            icon: 'check_circle'
          }).goAway(3500);
        })
        .catch((error) => {
          this.refreshing = false;
          Vue.toasted.error('Error Refreshing Data', {
            position: 'bottom-right',
            icon: 'report_problem'
          }).goAway(3500);
        });
    }
  }
}
</script>

<style>
.container
{
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.title
{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

  .align-center{
    margin: 0px auto;
    margin-top: 10px !important;
  }

</style>
