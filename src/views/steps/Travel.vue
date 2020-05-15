<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      In the last 14 days, have you travelled internationally?
    </p>
    <div class="content">
      <div class="travel" v-for="(travel, i) of travels" :key="travel.text" @click="selecttravel(i)">
        <div class="man">
          <span>
            {{ travel.text }}
          </span>
        </div>
        <div class="icn">
          <a-checkbox :checked="travel.selected"></a-checkbox>
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
        travels: [
          {
            text: 'Yes, I have',
            selected: false,
          },
          {
            text: 'No, I have not',
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
        return !this.travels.find((r) => r.selected)
      },
    },
    methods: {
      forward() {
        EventBus.$emit('next')
        let selected = this.travels.find((t) => t.selected)
        this.$store.commit('update_data', {
          type: 'travel',
          value: {
            text: selected.text,
            present: selected.text !== this.travels[this.travels.length - 1].text,
          },
        })
      },
      selecttravel(j) {
        this.travels = this.travels.map((r, i) => {
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
      if (this.state.travel) {
        this.travels = this.travels.map((t) => {
          return t.text === this.state.travel.text
            ? {
                ...t,
                selected: true,
              }
            : t
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
    .travel {
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
      .travel {
        width: 90%;
      }
    }
  }
</style>
