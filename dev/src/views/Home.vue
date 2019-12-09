<template>
  <div class="home">
    <div id="search-div">
      <h1>Welcome to Louisville Online Services</h1>
      <h2>How can we help you today?</h2>
      <input v-model="search" placeholder="Ex: 'Go To School', 'Get Dog', 'Report Crime'">
    </div>
    <button id="search-btn" v-on:click="filterServices">Search</button>
    <div id="results" v-show="show" ref="results">
      <p>Results:</p>
      <template v-show="results.length > 0">
        <a class="service-result" v-for="service in results" v-bind:key="service.nid" :href="service.field_service_url" target="_blank">{{ service.node_title }}</a>
      </template>
    </div>
    <div id="featured">
      <p>Featured:</p>
      <template v-if="featured.length > 0">
        <a class="service" v-for="service in featured" v-bind:key="service.nid" :href="service.field_service_url" target="_blank">{{ service.node_title }}</a>
      </template>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Home',
  data(){
    return {
      services: null,
      search: '',
      featured: {},
      results: [],
      show: false
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
          this.results = response.data;
          let rn1 = Math.floor(Math.random() * response.data.length);
          let rn2 = Math.floor(Math.random() * response.data.length);
          let rn3 = Math.floor(Math.random() * response.data.length);
          this.featured = [response.data[rn1], response.data[rn2], response.data[rn3]];
        })
    },
    filterServices(){
      /* eslint-disable no-console */
      this.show = true;
      let input, filter, list, items;
      input = this.search;
      filter = input.toUpperCase();
      list = document.getElementById('results');
      items = list.getElementsByClassName("service-result");
      console.log(items);
      for (let i = 0; i < items.length; i++) {
        if (items[i].innerHTML.toUpperCase().indexOf(filter) > -1) {
          items[i].style.display = "";
          break;
        } else {
          items[i].style.display = "none";
        }
      }
    }
  }

}
</script>

<style lang="scss" scoped>
@import "../stylesheets/theme";
.home {
  display: flex;
  flex-direction: column;
  justify-content: center;

  #search-btn {
    align-self: center;
    width: 30%;
    background-color: color(highlight);
    border-radius: 50px;
    border: none;
    color: color(tColor);
    padding: 15px;
    font-size: 25px;
    font-family: font(sFont);

    &:hover {
      background-color: darken($color: color(highlight), $amount: 10);
      cursor: pointer;
    }
    
    &:focus {
      outline: none;
    }
  }
}

#search-div {

  h1,h2 {
    padding: 15px;
  }

  h1 {
    font-family: font(sFont);
    font-size: 30px;
    letter-spacing: 1px;
  }

  h2 {
    font-size: 70px;
    color: darken($color: color(pColor), $amount: 10);
  }

  input {
    margin: 25px 0;
    padding: 20px;
    border-radius: 50px;
    width: 80%;
    font-family: font(pFont);
    border: none;

    &:focus {
      outline: none;
      box-shadow: 0 0 5px 1px color(shadow);
    }
  }
}

#featured {
  width: 80%;
  padding: 10px;
  display: flex;
  align-self: center;
  margin-top: 10px;

  .service {
    margin: 10px;
    width: 33.33%;
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

#results {
  width: 80%;
  padding: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-self: center;

  .service-result {
    margin: 10px;
    background-color: #9324a0;
    position: relative;
    padding: 20px;
    border-radius: 50px;
    color: color(tColor);
    text-decoration: none;
    box-shadow: 0 0 5px 1px color(shadow);

    &:hover {
      background-color: darken($color: #9324a0, $amount: 10);
    }
  }
}
</style>
