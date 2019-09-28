<template>
  <div>
    <h3>Hello dog</h3>
    <div>
      <select v-on:change="getDog" v-model="selectedBreed">
       <option value="">Select</option>
       <option value="breed" v-for="(value, breed) in breeds" v-bind:key="breed">
       {{ breed }}
       </option>
      </select>
    </div>
    <button v-on:click="getDog">
    <img v-show='dogUrl' v-bind:src="dogUrl" alt="Dog-image">
    </button>
  </div>
</template>

<script>
export default {
  name: 'HelloDog',
  data(){
    return {
      dogUrl: null,
      breeds: null,
      selectedBreed: ''
    }
  },
  created(){
      this.getDog();
      this.getBreeds();
  },
  methods: {
    getDog(){
      fetch('https://dog.ceo/api/breeds/image/random')
      .then(res => res.json())
      .then(data => this.dogUrl = data.message);  
    },
    getBreeds(){
      fetch('https://dog.ceo/api/breeds/list/all')
      .then(res => res.json())
      .then(data => this.breeds = data.message);  
    }
  }
}
</script>

<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
button {
  background: none;
  border: none;
}
</style>
