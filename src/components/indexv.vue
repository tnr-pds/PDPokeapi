<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">PD-Poke</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <!-- <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item> -->
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input
              input
              type="text"
              name=""
              id=""
              placeholder="Enter ID Pokamon 1-898"
              v-model="idpoke"
            ></b-form-input>
            <!-- <b-button type="button" value="" @click="loadId">Search ID</b-button> -->
            <b-button type="button" value="" @click="loadName"
              >Load Pokemon Info</b-button
            >
          </b-nav-form>

          <!-- <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">ES</b-dropdown-item>
            <b-dropdown-item href="#">RU</b-dropdown-item>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown> -->

          <!-- <b-nav-item-dropdown right> -->
          <!-- Using 'button-content' slot -->
          <!-- <template #button-content>
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown> -->
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
    <!-- <h1>{{ namepoke }}</h1>
    <h2>Ability: {{ abilitypoke2 }}</h2>
    <img :src="`${pokeImgfm}`" alt="" />
    <img :src="`${pokeImgbm}`" alt="" />
    <img :src="`${pokeImgff}`" alt="" />
    <img :src="`${pokeImgbf}`" alt="" />
    <h2>{{ abilitypoke1 }}</h2>
    <h3>Height: {{ pokeheight }} Inches.</h3>
    <h3>Weight: {{ pokeweight }} Kilograms.</h3> -->
        <!-- {{ pokeinfo }} -->

        <!-- <ul v-for="user in userList" :key="user.id" >
     <li>id:{{user.id}} name:{{user.name}} email:{{user.email}} ที่อยู่:{{user.address.geo}}
     <a :href = "`https://www.google.com/maps/search/${user.address.geo.lat},${user.address.geo.lng}`" >ที่อยู่</a> 
     </li>
     </ul> -->

    <div class="card text-center">
      <div class="card-header">
        <h2>{{ namepoke }}</h2>
      </div>
      <div class="card-body">
        <img :src="`${pokeImgfm}`" alt="" />
        <img :src="`${pokeImgbm}`" alt="" />
        <img :src="`${pokeImgff}`" alt="" />
        <img :src="`${pokeImgbf}`" alt="" />
        <h5 class="card-title">Ability: {{ abilitypoke2 }}</h5>
        <h5 class="card-title">Height: {{ pokeheight }} Inches</h5>
        <h5 class="card-title">Weight: {{ pokeweight }} Kilograms.</h5>
        <!-- <p class="card-text">
          With supporting text below as a natural lead-in to additional content.
        </p> -->
        <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
      </div>
      <div class="card-footer text-muted"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      pokeinfo: null,
      url: "https://pokeapi.co/api/v2/pokemon/",
      idpoke: null,
      namepoke: null,
      pokeImgfm: "",
      pokeImgbm: "",
      pokeImgff: "",
      pokeImgbf: "",
      pokeheight: null,
      pokeweight: null,
      abilitypoke1: "",
      abilitypoke2: "",
    };
  },
  methods: {
    loadId() {
      axios
        .get(this.url + this.idpoke)
        .then((response) => {
          this.pokeinfo = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    loadName() {
      axios
        .get(this.url + this.idpoke)
        .then((response) => {
          this.namepoke = response.data.forms[0].name;
          this.pokeImgfm = response.data.sprites.front_default;
          this.pokeImgbm = response.data.sprites.back_default;
          this.pokeImgff = response.data.sprites.front_shiny;
          this.pokeImgbf = response.data.sprites.back_shiny;
          this.abilitypoke1 = response.data.abilities[0].ability.name;
          this.abilitypoke2 = response.data.abilities[1].ability.name;
          this.pokeheight = response.data.height;
          this.pokeweight = response.data.weight;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>