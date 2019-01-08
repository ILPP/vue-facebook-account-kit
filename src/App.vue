<template>
  <div id="app">
    <facebook-account-kit ref="accountKit"
      appId="2310458705850799"
      version="v1.0"
      :fbAppEventsEnabled='true'
      :debug='true'
      :loginType='loginType'
      state="qinghuan">
      <select v-model="loginType">
        <option disabled value="">choose one</option>
        <option value="EMAIL">EMAIL</option>
        <option value="PHONE">PHONE</option>
      </select>
      <div v-if="loginType == 'PHONE'">
        <input value="+86" id="country_code" v-model="countryCode" />
        <input placeholder="phone number" id="phone_number" v-model="phoneNumber"/>
      </div>
      <div v-if="loginType == 'EMAIL'">
        <input placeholder="email" id="email" v-model="emailAddress"/>
      </div>
      <button @click="login()">Login</button>
    </facebook-account-kit>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      loginType: "PHONE",
      emailAddress: "",
      countryCode: "+86",
      phoneNumber: ""
    };
  },
  methods: {
    login() {
      console.log(this.$refs);
      this.$refs.accountKit.login(
        {
          countryCode: this.countryCode,
          phoneNumber: this.phoneNumber
          // emailAddress: this.emailAddress,
          // display: "modal"
        },
        this.loginCallback
      );
    },
    loginCallback(response) {
      console.log(response);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
