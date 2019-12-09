<template>
  <div id="app">
    <div id="nav">
      <router-link to="/" id="logo"><img alt="OD logo" src="./assets/logo.svg"></router-link>
      <router-link to="/services" id="services-btn">List of Services</router-link>
    </div>
    <router-view/>
    <div id="watermark">POWERED BY
      <a href="https://data.louisvilleky.gov/">
        <img src="./assets/logo.png" alt="LOUISVILLE OPEN DATA logo">
      </a>
    </div>
  </div>
</template>

<script>

</script>

<style lang="scss">
// Reset CSS
@import "./stylesheets/reset";
// Theme
@import "./stylesheets/theme";
#app {
  font-family: font(pFont);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: color(tColor);
  background-color: #ffffff;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100%25' height='100%25' viewBox='0 0 800 800'%3E%3Cg %3E%3Ccircle fill='%23ffffff' cx='400' cy='400' r='600'/%3E%3Ccircle fill='%23d0cfdc' cx='400' cy='400' r='500'/%3E%3Ccircle fill='%23a2a1ba' cx='400' cy='400' r='400'/%3E%3Ccircle fill='%23757698' cx='400' cy='400' r='300'/%3E%3Ccircle fill='%234a4d78' cx='400' cy='400' r='200'/%3E%3Ccircle fill='%231c2859' cx='400' cy='400' r='100'/%3E%3C/g%3E%3C/svg%3E");
  background-attachment: fixed;
  background-size: cover;
  min-height: 100vh;
}

#nav {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;

  @include medium {
    flex-direction: row;
    justify-content: space-between;
  }

  a {
    text-decoration: none;

    &.router-link-exact-active {
      color: color(tColor);
    }
  }

  #logo {
    img {
      height: 80px;
      filter: drop-shadow(0 0 6px color(shadow));
    }
  }

  #services-btn {
    padding: 20px;
    background-color: color(sColor);
    border-radius: 50px;
    color: color(tColor);
    font-family: font(pFont);
    box-shadow: 0 0 5px 1px color(shadow);
    font-weight: 0;

    &:hover {
      background-color: darken($color: color(sColor), $amount: 10);
    }
  }
}

#watermark{
  position: fixed;
  bottom: 0;
  right: 0;
  padding: 10px;
  filter: opacity(0.5);

  img {
    width: 300px;
  }
}
</style>