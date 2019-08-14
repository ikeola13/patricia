<template>
  <div class="hello">
    <div class="cardd">
      <div class="one">My Tasks</div>
      <div class="two">{{totalcheck}} of {{totalitems}} Tasks</div>
      <hr />
      <ul>
        <li v-for="item in items" :key="item.id">
          <input
            type="checkbox"
            v-model="item.completed"
            v-bind:id="item.id"
            v-bind:value="item.id"
            v-on:change="filterMedia(item.completed)"
          />
          <label class="strikethrough">{{item.title}}</label>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      items: [],
      msg: "Welcome to Your Vue.js App"
    };
  },
  mounted() {
    const baseURI = "https://jsonplaceholder.typicode.com/todos/";
    this.$http.get(baseURI).then(result => {
      this.items = result.data;
      //   this.totalcheck = result.data.completed.length;
      this.totalitems = result.data.length;
      console.log(result.data);
      console.log(result.data.length);

      const x = result.data.filter(o => o.completed === true);
      console.log(x.length);
      this.totalcheck = x.length;
    });
  },
  methods: {
    fetchUsers: function() {
      const baseURI = "https://jsonplaceholder.typicode.com/users";
      this.$http.get(baseURI).then(result => {
        this.users = result.data;
        console.log(result);
      });
    },
    filterMedia(it) {
      if (it === true) {
        this.totalcheck++;
      }

      if (it === false) {
        this.totalcheck--;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
  text-align: left;
}
li {
  margin: 10px 10px;
}
a {
  color: #42b983;
}
.cardd {
  padding: 30px;
  border: 1px solid black;
  width: 30%;
  margin: 0 auto;
  margin-top: 60px;
}
label {
  display: initial;
  margin-bottom: 0.5rem;
  padding-left: 10px;
}

input[type="checkbox"]:checked + .strikethrough {
  text-decoration: line-through;
}
.one {
  text-align: right;
  font-size: 30px;
  font-weight: 700;
}
.two {
  text-align: right;
}
@media only screen and (max-width: 600px) {
  .cardd {
    padding: 30px;
    border: 1px solid black;
    width: 85%;
    margin: 0 auto;
    margin-top: 60px;
  }
}
</style>
