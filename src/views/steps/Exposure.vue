<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      In the last 14 days, have you been in an exposure where COVID-19 is widespread?
    </p>
    <div class="content">
      <div class="exposure" v-for="(exposure, i) of exposures" :key="exposure.text" @click="selectexposure(i)">
        <div class="man">
          <span>
            {{ exposure.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="exposure.selected"></a-checkbox>
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
        exposures: [
          {
            text: 'Yes, I live with someone who has',
            selected: false,
          },
          {
            text: 'Yes, I have had close contact someone who has',
            selected: false,
          },
          {
            text: 'Yes, I have been near someone who has',
            selected: false,
          },
          {
            text: 'No, I have had no exposure',
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
        return !this.exposures.find((r) => r.selected)
      },
    },
    methods: {
      forward() {
        EventBus.$emit('next')
        let selected = this.exposures.find((t) => t.selected)
        this.$store.commit('update_data', {
          type: 'exposure',
          value: {
            text: selected.text,
            present: selected.text !== this.exposures[this.exposures.length - 1].text,
          },
        })
      },
      selectexposure(j) {
        this.exposures = this.exposures.map((r, i) => {
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
      if (this.state.exposure) {
        this.exposures = this.exposures.map((exp) => {
          return exp.text === this.state.exposure.text
            ? {
                ...exp,
                selected: true,
              }
            : exp
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
    .exposure {
      width: 450px;
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
      .exposure {
        width: 90%;
      }
    }
  }
</style>
