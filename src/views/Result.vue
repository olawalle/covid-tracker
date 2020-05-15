<!-- @format -->

<template>
  <div class="result">
    <div class="hero">
      <p class="heading top">{{ state.name }} Self-Assessment Result</p>
      <p class="heading btm">
        The accredicted disease control centre in your country will be in touch with further details.
      </p>
    </div>
    <div class="actions">
      <img src="../assets/back.svg" alt="" @click="toLast()" />
      <div class="blues">
        <img src="../assets/printer.svg" alt="" />
        <span>Done</span>
      </div>
    </div>
    <div class="contents">
      <div class="nextsteps">
        <p class="titlee">{{ admin ? `${state.name.split(' ')[0]}'s` : 'Your' }} Next Steps</p>
        <div class="single" v-for="(step, i) in steps" :key="step.title">
          <div class="no">
            <div>
              {{ i + 1 }}
            </div>
          </div>
          <div class="texts">
            <p class="text-title">
              {{ step.title }}
            </p>
            <p class="text-content">
              {{ step.content }}
            </p>
          </div>
        </div>
      </div>
      <div class="rightside">
        <div class="contact" v-if="admin">
          <p class="titlee">
            Contact Details
          </p>
          <span>
            Phone Number: +234809842355
          </span>
          <span>
            Email: testing@medical.com
          </span>
          <span> Address: 433 Lugard Street, Federal Road, Ekiti</span>
        </div>
        <div class="responses">
          <p class="titlee">{{ admin ? `${state.name.split(' ')[0]}'s` : 'Your' }} Responses</p>

          <ul>
            <li><span>-</span> You are {{ !state.symptoms.present ? 'not' : '' }} experiencing symptoms</li>
            <li><span>-</span> You {{ !state.conditions.present ? 'do not' : '' }} have relevant conditions</li>
            <li><span>-</span> You have {{ !state.travel.present ? 'not' : '' }} traveled internationally</li>
            <li><span>-</span> You have {{ !state.area.present ? 'not' : '' }} been to an area where it’s widespread</li>
            <li><span>-</span> You have {{ !state.exposure.present ? 'not' : '' }} been exposed to others who are sick</li>
            <li><span>-</span> You {{ !state.facility.present ? 'do not' : '' }} live or work in a care facility</li>
          </ul>
          <p class="footer">Completed {{ dayjs().format('MMM DD YYYY, hh:mm a') }} Privacy Policy</p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  import EventBus from '../eventbus'
  import { mapGetters } from 'vuex'
  import * as dayjs from 'dayjs'
  export default {
    data() {
      return {
        admin: false,
        steps: [
          {
            title: 'Isolate From Others',
            content:
              'You should try to stay away from others for at least 7 days from when your symptoms first appeared. Your isolation can end if your symptoms improve significantly and if you have had no fever for at least 72 hours without the use of medicine. By isolating yourself, you can slow the spread of COVID-19 and protect others.',
          },
          {
            title: 'Rest and Take Care',
            content: 'Eat well, drink fluids, and get plenty of rest.',
          },
          {
            title: 'Call Your Work Health Provider',
            content:
              'You should notify your work of your current symptoms as quickly as you can. This is vital to slowing the spread of COVID-19.',
          },
          {
            title: 'Monitor Symptoms',
            content:
              'Watch for COVID-19 symptoms such as cough, fever, and difficulty breathing. If your symptoms get worse, contact your doctor’s office.',
          },
          {
            title: 'Talk to Someone About Testing',
            content:
              'Your answers suggest you may need to get tested for COVID-19. You should get in touch with your doctor’s office or your state or local health department for more information. Testing access may vary by location and provider.',
          },
        ],
      }
    },
    computed: {
      ...mapGetters({
        state: 'getState',
      }),
    },
    mounted() {
      this.admin = this.$route.params.role === 'admin'
    },
    methods: {
      dayjs,
      toLast() {
        // EventBus.$emit('last')
        this.$router.push('/')
      },
    },
  }
</script>
<style lang="scss" scoped>
  .result {
    .hero {
      height: 250px;
      width: 100%;
      background: #fafafa;
      text-align: center;
      padding-top: 70px;
      .top {
        font-size: 30px;
        width: 40%;
        margin: 0 auto;
      }
      .btm {
        font-size: 18px;
        width: 40%;
        margin: 0 auto;
        margin-top: 10px;
      }
    }
    .actions {
      padding: 40px 100px;
      img {
        cursor: pointer;
      }
      .blues {
        float: right;
        color: #0066ff;
        span {
          margin-left: 20px;
          cursor: pointer;
        }
      }
    }
    .contents {
      padding: 0 100px;
    }
    .nextsteps {
      padding: 15px 50px 0 0;
      width: 55%;
      float: left;
      .titlee {
        font-size: 20px;
        line-height: 37px;
        letter-spacing: 0.005em;
        color: #413c3c;
        font-weight: 600;
      }
      .single {
        border-bottom: 1px solid #c4c4c4;
        padding: 30px 0;
        .no {
          width: 40px;
          float: left;
          div {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            font-weight: 600;
            font-size: 20px;
            line-height: 40px;
            text-align: center;
            color: #413c3c;
            border: 1px solid #c4c4c4;
          }
        }
        .texts {
          //   float: left;
          text-align: left;
          .text-title {
            font-weight: 600;
            font-size: 18px;
            line-height: 33px;
            letter-spacing: 0.005em;
            color: #413c3c;
            padding-left: 60px;
            margin-bottom: 5px;
          }
          .text-content {
            font-size: 14px;
            line-height: 28px;
            letter-spacing: 0.005em;
            color: #413c3c;
            font-weight: 300;
            padding-left: 60px;
            margin-bottom: 0;
          }
        }
      }
    }
    .rightside {
      width: 45%;
      float: left;
      .contact {
        border: 1px dashed #0066ff;
        padding: 40px;
        background: #fafafa;
        border-radius: 8px;
        margin-bottom: 30px;
        .titlee {
          font-size: 20px;
          line-height: 37px;
          letter-spacing: 0.005em;
          color: #0066ff;
          font-weight: 600;
          margin-bottom: 10px;
        }
        span {
          display: block;
          font-size: 14px;
          line-height: 28px;
          letter-spacing: 0.005em;
          color: #413c3c;
          margin-bottom: 5px;
        }
      }
      .responses {
        padding: 40px;
        background: #fafafa;
        border: 1px solid rgba(196, 196, 196, 0.5);
        border-radius: 8px;
        .titlee {
          font-size: 20px;
          line-height: 37px;
          letter-spacing: 0.005em;
          color: #413c3c;
          font-weight: 600;
        }
        ul {
          padding: 0;
          li {
            list-style-type: none;
            margin-top: 12px;
            color: #413c3c;
            span {
              padding-right: 6px;
            }
          }
        }
        .footer {
          font-size: 14px;
          line-height: 28px;
          letter-spacing: 0.005em;
          color: #c4c4c4;
          margin-top: 40px;
          font-weight: 200;
        }
      }
    }

    @media (max-width: 767px) {
      .hero {
        padding-top: 30px;
        .top {
          font-size: 26px;
          width: 86%;
        }
        .btm {
          font-size: 18px;
          width: 80%;
        }
      }
      .actions {
        padding: 40px 20px;
      }
      .contents {
        padding: 0 20px;
      }
      .nextsteps {
        width: 100%;
        padding: 0;
      }
      .rightside {
        width: 100%;
        margin-top: 30px;
        .responses,
        .contact {
          padding: 30px;
        }
      }
      .titlee {
        margin-bottom: 0;
      }
    }
  }
</style>
