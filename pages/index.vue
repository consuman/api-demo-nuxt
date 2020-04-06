<template>
  <div class="container">
    <div>
      <h1>Read Data:</h1>
      <p> {{ fromApi }} </p>
      <br>
      <button class="button" @click="postSomething()">Post Data to API</button>
    </div>

  </div>
</template>

<script>
export default {
  mounted() {
    this.getSomething();
  },
  data() {
    return {
      fromApi: '',
      headers: {
        'Content-Type': 'application/json',
        'access-token': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjaGVjayI6dHJ1ZSwiaWF0IjoxNTg2MTYzMjAxLCJleHAiOjE2MTc2OTkyMDF9.vot4mfiR0j6OewlJ0RWgRksDGp-BSD4RPSymZpXTjAs'
      }
    }
  },
  methods: {
    async getSomething() {
      let requested = {};
      let requestedRaw = await this.$axios.get('/my-api/', {
         headers: this.headers
      }).then(value => requested = value.data);
      console.log(requested);
      this.fromApi = requested;
    },
    postSomething() {
      const data = { testData: 'API Data overwritten!' };
      this.$axios.post('/my-api/', data, {
        headers: this.headers
      });
      console.log(data);
      this.getSomething();
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
.button {
  font-size: 30px;
}
</style>
