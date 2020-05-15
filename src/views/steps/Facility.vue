<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Do you live or work in a care facility?
    </p>
    <div class="content">
      <div class="facility" v-for="(facility, i) of facilities" :key="facility.text" @click="selectfacility(i)">
        <div class="man">
          <span>
            {{ facility.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="facility.selected"></a-checkbox>
        </div>
      </div>
      <br />
      <button class="main-btn" @click="forward()" style="margin-top: 0;" :disabled="disableBtn">Continue</button>
    </div>
  </div>
</template>
<script>
  import EventBus from '../../eventbus'
  import { mapGetters } from 'vuex'
  export default {
    data() {
      return {
        facilities: [
          {
            text: 'Yes, I live in a long-term care facility',
            selected: false,
          },
          {
            text: 'Yes, I have in the past 14 days',
            selected: false,
          },
          {
            text: 'No, but I plan to in the next 14 days',
            selected: false,
          },
          {
            text: 'No, I do not live or work in a care facility',
            selected: false,
          },
        ],
      }
    },
    computed: {
      ...mapGetters({
        state: 'getState',
      }),
      disableBtn() {
        return !this.facilities.find((r) => r.selected)
      },
    },
    methods: {
      forward() {
        let facility = this.facilities.find((s) => s.selected).text
        let present = facility !== this.facilities[this.facilities.length - 1].text
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'facility',
          value: {
            facility,
            present,
          },
        })
      },
      selectfacility(j) {
        this.facilities = this.facilities.map((r, i) => {
          return i === j
            ? {
                ...r,
                selected: true,
              }
            : {
                ...r,
                selected: false,
              }
        })
      },
    },
    mounted() {
      let stateFacility = this.state.facility
      if (stateFacility) {
        this.facilities = this.facilities.map((s) => {
          return stateFacility.facility === s.text
            ? {
                ...s,
                selected: true,
              }
            : s
        })
      }
    },
  }
</script>
<style lang="scss" scoped>
  .heading {
    width: 600px;
  }
  .content {
    text-align: center;
    .selected {
      background: #fafafa;
    }
    .facility {
      width: 400px;
      height: 55px;
      margin: 0 auto;
      line-height: 55px;
      border: 1px solid #c4c4c4;
      box-sizing: border-box;
      border-radius: 8px;
      text-align: left;
      padding: 0 20px;
      margin-bottom: 12px;
      cursor: pointer;
      transition: linear all 0.3s;
      .man {
        display: inline-block;
        height: 100%;
        line-height: 0;
        margin-top: 8px;
        text-transform: uppercase;
        span {
          display: block;
          margin-top: 15px;
          font-weight: 600;
          color: #413c3c;
        }
      }
      .icn {
        float: right;
      }
    }
  }

  @media (max-width: 767px) {
    .heading {
      margin-top: 0 !important;
    }
    .content {
      .facility {
        width: 90%;
      }
    }
  }
</style>
