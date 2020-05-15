<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Great to meet you Jolayemi! What’s your home address?
    </p>
    <div class="content">
      <a-select defaultValue="Nigeria" v-model="country" size="large" class="country">
        <a-select-option v-for="country in countries" :value="country.country" :key="country.country">{{
          country.country
        }}</a-select-option>
      </a-select>

      <a-input v-model="address" size="large" placeholder="STREET ADDRESS, CITY, STATE" />
      <img src="../../assets/mapmarker.svg" alt="" class="map" />
      <br />

      <button class="main-btn" @click="forward()" :disabled="disableBtn">Continue</button>
    </div>
  </div>
</template>
<script>
  import EventBus from '../../eventbus'
  import { mapGetters } from 'vuex'
  export default {
    data() {
      return {
        country: 'Nigeria',
        address: '',
      }
    },
    computed: {
      ...mapGetters({
        countries: 'getCountries',
        state: 'getState',
      }),
      disableBtn() {
        return !this.country || !this.address
      },
    },
    mounted() {
      if (this.state.address) {
        this.country = this.state.address.country
        this.address = this.state.address.state
      }
    },
    methods: {
      forward() {
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'address',
          value: {
            country: this.country,
            state: this.address,
          },
        })
      },
    },
  }
</script>
<style lang="scss" scoped>
  .heading {
    width: 550px;
  }
  .content {
    position: relative;
    .country {
      width: 200px;
    }
    .map {
      position: absolute;
      left: 265px;
      margin-top: 10px;
      width: 22px;
    }
    input {
      width: 400px !important;
      padding-left: 50px;
    }
  }

  @media (max-width: 767px) {
    .content {
      .country {
        width: 30% !important;
      }
      .map {
        left: 40%;
      }
      input {
        width: 63% !important;
        float: right !important;
      }
    }
  }
</style>
