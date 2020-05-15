<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      In the last 14 days, have you been in an area where COVID-19 is widespread?
    </p>
    <div class="content">
      <div class="area" v-for="(area, i) of areas" :key="area.text" @click="selectarea(i)">
        <div class="man">
          <span>
            {{ area.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="area.selected"></a-checkbox>
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
        areas: [
          {
            text: 'Yes, I have',
            selected: false,
          },
          {
            text: 'No, I have not',
            selected: false,
          },
          {
            text: 'I do not know',
            selected: false,
          },
          {
            text: 'None of the above',
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
        return !this.areas.find((r) => r.selected)
      },
    },
    methods: {
      forward() {
        let area = this.areas.find((s) => s.selected).text
        let present = area !== this.areas[this.areas.length - 1].text
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'area',
          value: {
            area,
            present,
          },
        })
      },
      selectarea(j) {
        this.areas = this.areas.map((r, i) => {
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
      let stateAreas = this.state.area
      if (stateAreas) {
        this.areas = this.areas.map((s) => {
          return stateAreas.area === s.text
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
    .area {
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
      .area {
        width: 90%;
      }
    }
  }
</style>
