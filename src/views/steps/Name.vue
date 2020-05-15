<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Hello I’m Aminat, from the Africa Tech Response team for COVID-19. Ready to get started?
    </p>
    <div class="content">
      <a-input v-model="firstname" placeholder="FIRSTNAME" size="large" />
      <a-input v-model="lastname" placeholder="LASTNAME" size="large" />
      <br />

      <button class="main-btn" :disabled="disableBtn" @click="forward()">Continue</button>
    </div>
  </div>
</template>
<script>
  import EventBus from '../../eventbus'
  import { mapGetters } from 'vuex'
  export default {
    data() {
      return {
        firstname: '',
        lastname: '',
      }
    },
    computed: {
      ...mapGetters({
        state: 'getState',
      }),
      disableBtn() {
        return !this.firstname || !this.lastname
      },
    },
    methods: {
      forward() {
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'name',
          value: `${this.firstname} ${this.lastname}`,
        })
      },
    },
    mounted() {
      if (this.state.name) {
        this.firstname = this.state.name.split(' ')[0]
        this.lastname = this.state.name.split(' ')[1]
      }
    },
  }
</script>
<style lang="scss" scoped>
  .heading {
    width: 700px;
  }
</style>
