<template>
  <div>
    <!--    名子的部分-->
    <div>
      <div>
        <p>firstName:</p>
        <input v-model="firstname"  @change="updateItem_person">
        {{firstname}}

      </div>
      <div>
        <p>lastName:</p>
        <input v-model="lastname"  v-on:change="updateItem_person">
        {{lastname}}
      </div>
    </div>
    <!--    性別-->
    <p>Gender</p>
    <input type="radio" id="male" value="0" v-model="sex_picked" v-on:change="updateItem_person">
    <label for="one">male</label>
    <br>
    <input type="radio" id="female" value="1" v-model="sex_picked" v-on:change="updateItem_person">
    <label for="two">female</label>
    <br>
    <input type="radio" id="secret" value="2" v-model="sex_picked" v-on:change="updateItem_person">
    <label for="two">secret</label>
    <br>
    <span>Picked: {{ sex_picked }}</span>
    <!--    地址-->
    <p>address</p>
    <input v-model="address" placeholder="edit me" :disabled="isHomeLess" v-on:change="updateItem_person">{{ isHomeLess }}
    <input type="checkbox" id="checkbox" v-model="isHomeLess" v-on:change="clearAddress">
    <label for="checkbox">此顧客暫無居所</label>

    <!--    工作-->
    <p>job</p>
    <select v-model="job" v-on:change="updateItem_person">
      <option v-for="job in jobs" v-bind:value="job.chi" v-bind:key="job.chi" >
        {{ job.chi }}
      </option>
    </select>
    {{job}}
    <!--    Note筆記-->
    <p>note</p>
    <p>{{ noteText.length }}/200 個字</p>
    <textarea v-model="noteText" placeholder="add multiple lines" maxlength="200" v-on:change="updateItem_person"></textarea>
    <!--    -->
  </div>


</template>

<script>
export default {
  props: {
    test: {type: String, require: true},
    totalPageData: {type: Array}
  },
  data: function () {
    return {
      firstname: '',
      lastname: '',
      address: "",
      isHomeLess: false,
      sex_picked: '',
      noteText: '',
      job:'',
      jobs: [{chi: "保密", eng: "null"}, {chi: "調查員", eng: "agent"}, {
        chi: "秘密調查員",
        eng: "secret_agent"
      }, {chi: "秘密調查員的調查員", eng: "agent_of_secret_agent"}]
    };
  },
  methods: {
    clearAddress: function () {
      const addressTag = this.$refs.el;
      if (this.$data.isHomeLess) {
        this.$data.address = '';
        addressTag.disable = true;
      } else {
        addressTag.disable = false;
      }
    },
    updateItem_person: function () {
      //事件名稱 //value =>this.message是指子層的噢！
      const data={"firstname":this.firstname,"lastname":this.lastname,"address":this.address,
        "sex_picked":this.sex_picked,"noteText":this.noteText,"jobs":this.job}
      this.$emit('person', data);
    }
  }
};
</script>

<style scoped>
p {
  font-size: 14px;
  text-align: center;
}
</style>