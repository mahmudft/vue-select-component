<template>
  <div>
    <h4>Dropdown Select Box</h4>
    <br />
    <!--Multi Input -->
    <div v-if="multi" class="multi">
      <div v-for="(tag, index) in tags" :key="index" class="multi_tag">
        <span @click="removetag(index)">x</span>
        {{ tag }}
      </div>
      <input
        type="text"
        @focus="showmultilist"
        v-model="multiinputdata"
        @input="multifilterdata"
        placeholder="search.."
        class="multi_tag_input"
      />
      <div v-if="multiactive" class="droplist">
        <h5 v-for="(item, key) in searchitems" :key="key" @click="addtag(item)">
          {{ item }}
        </h5>
      </div>
    </div>

    <!--Simgle Input -->
    <input
      v-else
      type="text"
      @focus="showlist"
      v-model="inputdata"
      @input="filterdata"
    />
    <div v-if="active" class="droplist">
      <h5 v-for="(item, key) in searchitems" :key="key" @click="setelem(item)">
        {{ item }}
      </h5>
    </div>
    <br />
    <div class="boxselector">
      <label for="multi">multisearch</label>
      <input id="multi" type="checkbox" v-model="multi" />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      tags: [],
      multi: false,
      multiactive: false,
      multiinputdata: "",
      active: false,
      searchitems: [],
      items: ["pink", "blue", "white", "dark"],
      curelement: "",
      inputdata: "",
    };
  },
  methods: {
    showlist() {
      this.searchitems = this.items;
      this.active = true;
    },
    hidelist() {
      this.active = false;
    },
    filterdata() {
      return (this.searchitems = this.items.filter((s) =>
        s.includes(this.inputdata)
      ));
      //console.log(event.target.value)
    },
    setelem(item) {
      this.curelement = item;
      this.active = false;
      this.inputdata = this.curelement;
    },
    testlink() {
      this.searchitems = this.items.filter((s) => s.includes(this.inputdata));
    },
    showmultilist() {
      this.searchitems = this.items;
      this.multiactive = true;
    },
    multifilterdata() {
      return (this.searchitems = this.items.filter((s) =>
        s.includes(this.multiinputdata)
      ));
    },
    addtag(item) {
      this.multiactive = false;
      this.multiinputdata = "";
      if(!this.tags.includes(item)) {
        this.tags.push(item);
      }
    },
    removetag(index) {
      this.tags.splice(index, 1);
    },
  },
  computed: {},
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  position: relative;
  width: 30%;
  text-align: left;
  outline: none;
  height: 20px;
  line-height: 10px;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  border-color: indigo;
  font-weight: bold;
}
.droplist {
  width: 30.4%;
  background-color: rgb(253, 253, 253);
  border-radius: 2px;
  margin: 0px;
  border: 2px solid indigo;
  overflow:hidden;
}
#showlist {
  display: flex;
  flex-direction: row;
}
h5:hover {
  background-color: orange;
}
h5 {
  font-weight: bold;
  border-color: 2px solid blueviolet;
  padding: 0px;
  margin: 4px;
  font-size: 18px;
}

.multi {
  width: 100%;
  border: 1px solid #eee;
  font-size: 0.9em;
  height: 50px;
  box-sizing: border-box;
  padding: 0 10px;
}

.multi_tag {
  height: 30px;
  float: left;
  margin-right: 10px;
  background-color: #eee;
  margin-top: 10px;
  line-height: 30px;
  padding: 0 5px;
  border-radius: 5px;
}

.multi_tag > span {
  cursor: pointer;
  opacity: 0.75;
}

.multi_tag_input {
  border: none;
  outline: none;
  font-size: 0.9em;
  line-height: 50px;
  background: none;
  max-width: 30%;
}

.boxselector {
  margin-top: 100px;
}
</style>
