<template>
  <div class="services">
    <template v-if="services.length > 0">
      <a class="service" v-for="service in services" v-bind:key="service.nid" :href="service.field_service_url" target="_blank">{{ service.node_title }}</a>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Services',
  data(){
    return {
      services: null
    }
  },
  mounted () {
    this.getServices();
  },
  methods: {
    getServices(){
      axios
        .get('https://cors-anywhere.herokuapp.com/https://louisvilleky.gov/services/toolbox_services.json?limit=0')
        .then( (response) => {
          this.services = response.data;
        })
    }
  }

}
</script>

<style lang="scss" scoped>
@import "../stylesheets/theme";
.services {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 0 50px;

  .service {
    margin: 10px;
    background-color: color(sColor);
    position: relative;
    padding: 20px;
    border-radius: 50px;
    color: color(tColor);
    text-decoration: none;
    box-shadow: 0 0 5px 1px color(shadow);

    &:hover {
      background-color: darken($color: color(sColor), $amount: 10);
    }
  }
}
</style>
