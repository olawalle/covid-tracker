<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Alright! Let’s get your result
    </p>
    <div class="content">
      <a-input v-model="email" placeholder="EMAIL ADDRESS" size="large" /> <br />
      <br />
      <a-input v-model="phone" placeholder="PHONE NUMBER" size="large" />
      <br />
      <br />

      <a-checkbox v-model="checked">I agree to the <span style="color: #0066ff;"> terms of service</span></a-checkbox>
      <br />

      <button class="main-btn" @click="finish()" :disabled="disableBtn">Continue</button>
    </div>
  </div>
</template>
<script>
  import { mapGetters } from 'vuex'
  export default {
    data() {
      return {
        email: '',
        phone: '',
        checked: false,
      }
    },
    computed: {
      ...mapGetters({
        state: 'getState',
      }),
      disableBtn() {
        return !this.email || !this.phone || !this.checked
      },
    },
    methods: {
      finish() {
        this.$router.push({
          name: 'Result',
          params: {
            role: 'user',
          },
        })
        this.$store.commit('update_data', {
          type: 'contact',
          value: {
            email: this.email,
            phone: this.phone,
          },
        })
      },
    },
    mounted() {
      if (this.state.contact) {
        this.email = this.state.contact.email
        this.phone = this.state.contact.phone
        this.checked = true
      }
    },
  }
</script>
<style lang="scss" scoped>
  .heading {
    width: 700px;
  }
  .content {
    input {
      width: 400px !important;
      margin-bottom: 20px;
    }
  }

  @media (max-width: 767px) {
    .heading {
      margin-top: 0 !important;
    }
    .content {
      input {
        width: 90% !important;
      }
    }
  }
</style>
