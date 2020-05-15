<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Are you experiencing any of these symptoms?
    </p>
    <div class="content">
      <div class="symptom" v-for="(symptom, i) of symptoms" :key="symptom.text" @click="selectsymptom(i)">
        <div class="man">
          <span>
            {{ symptom.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="symptom.selected"></a-checkbox>
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
        symptoms: [
          {
            text: 'Fever, chills or sweating',
            selected: false,
          },
          {
            text: 'Diffiulty breathing (not severe)',
            selected: false,
          },
          {
            text: 'New or worsening cough',
            selected: false,
          },
          {
            text: 'Sore throat',
            selected: false,
          },
          {
            text: 'Aching throughout the body',
            selected: false,
          },
          {
            text: 'VOMITING OR DIARRHEA',
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
        return !this.symptoms.find((r) => r.selected)
      },
      ...mapGetters({
        state: 'getState',
      }),
    },
    methods: {
      forward() {
        let shownSymptoms = this.symptoms.filter((s) => s.selected)
        let none = shownSymptoms.find((s) => s.text === 'None of the above')
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'symptoms',
          value: {
            symptoms: none ? [] : shownSymptoms,
            present: none ? false : true,
          },
        })
      },
      selectsymptom(j) {
        this.symptoms = this.symptoms.map((r, i) => {
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
      let stateSymptoms = this.state.symptoms
      if (stateSymptoms) {
        let obj = stateSymptoms.symptoms.reduce((agg, curr) => {
          agg[curr.text] = curr
          return agg
        }, {})
        this.symptoms = this.symptoms.map((s) => {
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
    .symptom {
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
      .symptom {
        width: 90%;
      }
    }
  }
</style>
