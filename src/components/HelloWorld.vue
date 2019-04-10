<template>
  <div class="hello">
    <div class="left">
      <h1>{{title}}</h1>
      <form action @submit.prevent="addLink">
        <input type="text" class="link-input" placeholder="Add a new link" v-model="newLink">
      </form>
      <ul>
        <li v-for="(link, index) in links" v-bind:key="index">
          {{link}}
          <button v-on:click="removeLinks(index)" class="rm">Remove</button>
        </li>
      </ul>
    </div>
    <div class="right">
      <stats/>
    </div>
  </div>
</template>

<script>
import Stats from "@/components/Stats.vue";
import { mapState, mapMutations, mapActions } from "vuex";

export default {
  name: "HelloWorld",
  data() {
    return {
      newLink: ""
    };
  },
  components: {
    Stats
  },
  computed: {
    ...mapState(["title", "links"])
  },
  methods: {
    ...mapMutations(["ADD_LINK"]),
    ...mapActions(["removeLink"]),
    addLink: function() {
      this.ADD_LINK(this.newLink);
      this.newLink = "";
    },
    removeLinks: function(link) {
      this.removeLink(link);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  color: #42b983;
}
</style>
