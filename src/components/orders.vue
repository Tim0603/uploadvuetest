<template>
  <div>
    <BUTTON v-on:click="updateText"></BUTTON>
    <h1>apple</h1>
    <button v-on:click="countapple(-5)">-5</button>
    <button v-on:click="countapple(-1)">-1</button>
    <input type="number" v-model="apple_count" v-on:change="inputApple;updateText;">
    <button v-on:click="countapple(1)">+1</button>
    <button v-on:click="countapple(5)">+5</button>

    <h1>banana</h1>
    <p>配料</p>
    <div v-for="fav in favorList" v-bind:value="fav.eng" v-bind:key="fav.chi">
      <input type="checkbox" v-model="picked_favor" v-bind:value="fav.chi" v-bind:key="fav.chi" @change="updateText">
      <label for="">{{ fav.chi }} </label>
    </div>
    <br>
    <span>Checked names: {{ picked_favor }}</span>

  </div>
</template>

<script>
export default {
  name: "",
  props: {
    test: {type: String, require: true},
    totalPageData: {type: Array},
    applecount: {type: Number},
    favor: {type: Array}
  },
  data: function () {
    return {
      picked_favor: this.favor,
      favorList: [{chi: "巧克力醬", eng: "chocolate"}, {chi: "草莓醬", eng: "strawberry"}, {chi: "胡麻醬", eng: "flax"},
        {chi: "味曾", eng: "miso"}, {chi: "辣椒", eng: "chili"}, {chi: "大蒜", eng: "garlic"}, {
          chi: "醬油",
          eng: "soy_sauce"
        }, {chi: "醬油膏", eng: "thick_soy_sauce"}, {chi: "百草膏", eng: "herbal_cream"}],
      apple_count: this.applecount
    }
  },
  methods: {
    countapple: function (mount) {
      if (!this.$data.apple_count) {
        this.$data.apple_count = 1
      }
      this.$data.apple_count = parseInt(this.$data.apple_count, 10)
      if (this.$data.apple_count < 1) {
        this.$data.apple_count = 1;
      } else if (this.$data.apple_count > 100) {
        this.$data.apple_count = 100;
      }
      this.$data.apple_count += parseInt(mount, 10)
      if (this.$data.apple_count < 1) {
        this.$data.apple_count = 1;
      } else if (this.$data.apple_count > 100) {
        this.$data.apple_count = 100;
      }
      this.updateText()
    },
    inputApple: function () {
      if (!this.$data.apple_count) {
        this.$data.apple_count = 1
      }
      this.$data.apple_count = parseInt(this.$data.apple_count, 10)
      if (this.$data.apple_count < 1) {
        this.$data.apple_count = 1;
      } else if (this.$data.apple_count > 100) {
        this.$data.apple_count = 100;
      }
      this.updateText()
    },
    updateText: function () {
      const data = {"picked_favor": this.picked_favor, "apple_count": this.apple_count}
      //事件名稱 //value =>this.message是指子層的噢！
      this.$emit('update', data);
    }
  }
}
</script>

<style scoped>
.btn {
  width: 15px;
  height: 15px;
}
</style>