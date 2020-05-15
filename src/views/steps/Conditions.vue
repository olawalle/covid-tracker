<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Do you have any of these conditions?
    </p>
    <div class="content">
      <div class="condition" v-for="(condition, i) of conditions" :key="condition.text" @click="selectcondition(i)">
        <div class="man">
          <span>
            {{ condition.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="condition.selected"></a-checkbox>
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
        conditions: [
          {
            text: 'Asthma or chronic lung disease',
            selected: false,
          },
          {
            text: 'Pregnancy',
            selected: false,
          },
          {
            text: 'Diabetes',
            selected: false,
          },
          {
            text: 'Kidney failure',
            selected: false,
          },
          {
            text: 'Cirrhosis of the liver',
            selected: false,
          },
          {
            text: 'Weakened immune system',
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
      disableBtn() {
        return !this.conditions.find((r) => r.selected)
      },
      ...mapGetters({
        state: 'getState',
      }),
    },
    methods: {
      forward() {
        let shownconditions = this.conditions.filter((s) => s.selected)
        let none = shownconditions.find((s) => s.text === this.conditions[this.conditions.length - 1].text)
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'conditions',
          value: {
            conditions: none ? [] : shownconditions,
            present: none ? false : true,
          },
        })
      },
      selectcondition(j) {
        this.conditions = this.conditions.map((r, i) => {
          return i === j
            ? {
                ...r,
                selected: !r.selected,
              }
            : {
                ...r,
              }
        })
      },
    },
    mounted() {
      let stateConditions = this.state.conditions
      if (stateConditions) {
        let obj = stateConditions.conditions.reduce((agg, curr) => {
          agg[curr.text] = curr
          return agg
        }, {})
        this.conditions = this.conditions.map((s) => {
          let preselected = obj[s.text]
          return preselected
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
    .condition {
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
      .condition {
        width: 90%;
      }
    }
  }
</style>
