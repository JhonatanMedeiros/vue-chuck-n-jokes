<template>
  <div class="joke-container">
    <h1>Vue Chuck Jokes</h1>
    <p>{{joke}}</p>
    <button type="button" v-if="!loading" @click="getJoke()">Random</button>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class ChuckJokes extends Vue {

  private api: string = 'https://api.chucknorris.io/jokes/random';

  private joke: string = '';

  private loading: boolean = false;

  private async mounted() {
    this.getJoke();
  }

  private getJoke() {
    this.loading = true;
    this.joke = 'Loading Joke...';
    axios.get(this.api)
      .then((res) => {
        const data = res.data;
        this.joke = data.value;
      })
      .catch((error) => {
        this.joke = 'OPS! Error.';
      })
      .finally(() => this.loading = false);
  }

}
</script>

<style scoped lang="scss">
.joke-container {
  button {
    display: inline-block;
    font-weight: 400;
    color: white;
    text-align: center;
    vertical-align: middle;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    border: 1px solid transparent;
    padding: .375rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    border-radius: .25rem;
    background-color: #42b983;
    cursor: pointer;
  }
}
</style>
