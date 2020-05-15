<!-- @format -->

<template>
  <div class="wrapping">
    <p class="heading">
      Hello I’m Aminat, from the Africa Tech Response team for COVID-19. Ready to get started?
    </p>
    <div class="content">
      <div class="range" v-for="(range, i) of ranges" :key="range.text" @click="selectRange(i)" :class="range.selected ? 'selected' : ''">
        <div class="man">
          <img src="../../assets/active-man.svg" alt="" v-if="range.selected" />
          <img src="../../assets/man.svg" alt="" v-else />
          <span>
            {{ range.text }}
          </span>
        </div>
        <div class="icn">
          <img src="../../assets/selected.svg" alt="" v-if="range.selected" />
          <img src="../../assets/not-selected.svg" alt="" v-else />
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
        ranges: [
          {
            text: 'UNDER 18',
            selected: false,
          },
          {
            text: 'BETWEEN 18 AND 64',
            selected: false,
          },
          {
            text: '65 OR OLDER',
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
        return !this.ranges.find((r) => r.selected)
      },
    },
    mounted() {
      if (this.state.age) {
        this.ranges = this.ranges.map((r) => {
          return r.text === this.state.age
            ? {
                ...r,
                selected: true,
              }
            : r
        })
        // this.country = this.state.address.country
        // this.address = this.state.address.state
      }
    },
    methods: {
      forward() {
        EventBus.$emit('next')
        this.$store.commit('update_data', {
          type: 'age',
          value: this.ranges.find((r) => r.selected).text,
        })
      },
      selectRange(j) {
        this.ranges = this.ranges.map((r, i) => {
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
    .range {
      width: 478px;
      height: 84px;
      margin: 0 auto;
      line-height: 84px;
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
      .range {
        width: 90%;
      }
    }
  }
</style>
