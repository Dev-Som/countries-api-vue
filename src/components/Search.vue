<template>
  <div class="wrapper">
    <div class="search">
      <div>
        <i class="fas fa-search"></i>
        <input
          type="text"
          placeholder="Search for a country..."
          v-model="search"
          @keyup="searching"
        />
      </div>
      <div></div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Search',
  data() {
    return {
      mode: true,
      countries: [],
      search: '',
      name: '',
      uri: 'https://restcountries.eu/rest/v2/region/europe',
    };
  },
  created() {
    return axios
      .get(this.uri)
      .then((response) => {
        this.countries = response.data;
        // console.log(response.data);
      })
      .catch((error) => {
        console.log(error);
      });
  },
  computed: {
    filteredCountries() {
      return this.countries.filter((country) => {
        return country.name.match(this.search);
      });
    },
  },
  methods: {
    searching() {
      this.$emit('change', this.search);
    },
  },
};
</script>

<style>
.wrapper {
  width: 90%;
  margin: 0 auto;
}
.light .search {
  background-color: var(--Very-Light-Gray-Background);
  color: var(--Very-Dark-Blue-Text);
  border: 2px solid #ccc;
}

.search {
  position: relative;
  display: flex;
  align-items: center;
  width: 30%;
  height: 40px;
  background-color: hsl(207, 26%, 17%);
  margin: 1rem;
  border-radius: 5px;
}

.search i {
  padding: 1rem;
  font-weight: 600;
}
input {
  outline: none;
  border: none;
  background: none;
  font-size: 12px;
  color: #fff !important;
  font-weight: 600;
}

@media (max-width: 768px) {
  .search {
    width: 90%;
  }
}
</style>
