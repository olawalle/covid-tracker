<!-- @format -->

<template>
  <div>
    <div class="header">
      <img src="../assets/back.svg" alt="" class="back" @click="previous()" v-if="step > 1" />
      <img src="../assets/user.png" alt="" class="user" />

      <div class="progress" v-if="step > 1">
        {{ doneCount }}% Progress

        <div class="wrap">
          <div class="indicator" :style="{ width: doneCount + '%' }"></div>
        </div>
      </div>
    </div>
    <div class="welcome">
      <Name v-if="step === 1" />
      <Address v-if="step === 2" />
      <Age v-if="step === 3" />
      <Symptoms v-if="step === 4" />
      <Conditions v-if="step === 5" />
      <Travel v-if="step === 6" />
      <Area v-if="step === 7" />
      <Exposure v-if="step === 8" />
      <Facility v-if="step === 9" />
      <Contact v-if="step === 10" />
    </div>
  </div>
</template>
<script>
  import Name from './steps/Name.vue'
  import Age from './steps/Age.vue'
  import Address from './steps/Address.vue'
  import Symptoms from './steps/Symptoms.vue'
  import Contact from './steps/Contact.vue'
  import Conditions from './steps/Conditions.vue'
  import Exposure from './steps/Exposure.vue'
  import Facility from './steps/Facility.vue'
  import Travel from './steps/Travel.vue'
  import Area from './steps/Area.vue'

  import Nav from '../components/Nav.vue'
  import Eventbus from '../eventbus'
  export default {
    data() {
      return {
        disableBtn: true,
        step: 1,
      }
    },
    components: {
      Name,
      Address,
      Age,
      Symptoms,
      Contact,
      Conditions,
      Exposure,
      Facility,
      Travel,
      Area,
      Nav,
    },
    computed: {
      doneCount() {
        return this.step < 10 ? this.step * 10 : 99
      },
    },
    methods: {
      refresh() {
        this.$confirm({
          title: 'Are you sure restart this test?',
          content: 'This action is irreversible.',
          okText: 'Yes',
          okType: 'danger',
          cancelText: 'No',
          onOk: () => {
            this.step = 1
          },
          onCancel: () => {},
        })
      },
      previous() {
        this.step = this.step - 1
      },
    },
    mounted() {
      Eventbus.$on('next', () => (this.step = this.step + 1))
      Eventbus.$on('refresh', () => (this.step = 1))
      // Eventbus.$on('last', () => (this.step = 10))
    },
  }
</script>

<style lang="scss">
  .welcome {
    .wrapping {
      width: 100%;
      text-align: center;
      .heading {
        color: #413c3c;
        font-size: 30px;
        margin: 0 auto;
      }
      .content {
        width: 700px;
        text-align: center;
        margin: 30px auto;
        input {
          width: 250px;
          // height: 50px;
          margin: 0 10px;
        }
        // .ant-select-selection--single {
        //   height: 50px;
        // }
        // .ant-select-selection-selected-value {
        //   height: 50px;
        //   line-height: 50px;
        // }
        button {
          margin-top: 20px;
        }
      }

      @media (max-width: 767px) {
        .heading {
          width: 90%;
          font-size: 20px;
          margin-top: 30px;
        }
        .content {
          width: 90%;
          text-align: center;
          margin: 30px auto;
          input {
            width: 46%;
            margin: 0 2%;
          }
        }
      }
    }
  }
</style>
