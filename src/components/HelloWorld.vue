<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <br />
    <a :href="api">Click Here to see content from API</a><br />
    <p>Click here for toggling to populate the table</p>
    <br /><button @click="trigger = !trigger">Go!</button>
    <br />
    <table v-if="trigger">
      <tr>
        <th>Index</th>
        <th>API</th>
        <th>Description</th>
        <th>Auth</th>
        <th>HTTPS</th>
        <th>Cors</th>
        <th>Link</th>
        <th>Category</th>
      </tr>
      <tr v-for="(data, index) in api_info" :key="index">
        <td>{{ index + 1 }}</td>
        <td>{{ data.API }}</td>
        <td>{{ data.Description }}</td>
        <td>{{ data.Auth }}</td>
        <td>{{ data.HTTPS }}</td>
        <td>{{ data.Cors }}</td>
        <td>
          <a :href="data.Link">{{ data.Link }}</a>
        </td>
        <td>{{ data.Category }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      api_info: [],
      trigger: false,
    };
  },
  props: {
    msg: String,
    api: String,
  },
  mounted() {
    axios
      .get(this.api)
      .then((res) => (this.api_info = res.data.entries))
      .catch((err) =>
        console.log(`Unable to process the request due to ${err}`)
      );
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  font-size: medium;
  color: #42b983;
  margin-bottom: 10px;
}
table,
th,
tr,
td {
  padding: 2px;
  border: 1px solid black;
}
</style>
