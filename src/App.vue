<!-- @format -->

<template>
  <div id="app">
    <Nav />
    <router-view />
  </div>
</template>

<script>
  import Nav from './components/Nav.vue'
  import EventBus from './eventbus'
  export default {
    components: {
      Nav,
    },
    methods: {
      previous() {},
    },
  }
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Alegreya:wght@400;500;700&family=Poppins:wght@200;300;400;500&display=swap');
  body {
    width: 100%;
  }
  #app {
    font-family: 'Poppins', sans-serif;
  }

  .heading {
    font-family: 'Alegreya', serif;
  }
  #nav {
    height: 70px;
    line-height: 70px;
    border-bottom: 2px solid #c4c4c4;
    padding: 0 50px;
    .logo {
      font-weight: 500;
      font-size: 24px;
      letter-spacing: 0.015em;
      color: #413c3c;
      float: left;
    }
    .icons {
      float: right;
      font-size: 20px;
      i {
        margin-left: 25px;
        cursor: pointer;
      }
    }
  }

  .header {
    width: 100%;
    height: 160px;
    padding: 40px 120px;
    position: relative;
    text-align: center;
    .back {
      // float: left;
      position: absolute;
      left: 120px;
      margin-top: 30px;
      cursor: pointer;
    }
    .progress {
      position: absolute;
      right: 120px;
      top: 50px;
      width: 120px;
      color: #c4c4c4;
      font-size: 14px;
      text-align: left;
      padding-top: 10px;
      display: inline-block;
      .wrap {
        width: 100%;
        height: 4px;
        background-color: #c4c4c4;
        border-radius: 15px;
        margin-top: 5px;
        .indicator {
          background-color: #0066ff;
          transition: linear all 0.3s;
          height: 4px;
          border-radius: 15px;
        }
      }
    }
  }

  @media (max-width: 767px) {
    #app {
      width: 100%;
      #nav {
        padding: 0 20px;
        .logo {
          font-size: 20px;
        }
        .icons {
          font-size: 20px;
        }
      }
      .header {
        width: 100%;
        padding: 20px;
        text-align: center;
        .back {
          left: 20px;
        }
        .progress {
          width: 100px;
          right: 20px;
          top: 35px;
        }
      }
    }
  }

  .main-btn {
    border: 0;
    width: 220px;
    height: 50px;
    color: #fff;
    background: #0066ff;
    border-radius: 5px;
    font-weight: 600;
    font-size: 14px;
    line-height: 50px;
    text-align: center;
    letter-spacing: 0.015em;
    text-transform: uppercase;
  }
  button:disabled {
    background: #c4c4c4;
    border-radius: 5px;
    cursor: not-allowed;
  }
</style>

<style lang="scss">
  .mytable {
    #myTable {
      margin-bottom: 0px !important;
      .ant-table-thead > tr {
        border-bottom: 20px solid #c4c4c438 !important;
      }
      .ant-table-thead > tr > th,
      .ant-table-tbody > tr > td {
        height: 25px !important;
        padding: 12px;
        font-size: 12px;
        background-color: #fff !important;
      }
      //   thead {
      //     background: #324e85 !important;
      //     tr {
      //       height: 25px !important;
      //       th {
      //         color: #ffffff !important;
      //         padding: 5px 5px !important;
      //         tbody {
      //           td {
      //             padding: 5px 5px !important;
      //             height: 25px !important;
      //             color: #324e85 !important;
      //             font-size: 11px !important;
      //           }
      //         }
      //       }
      //     }
      //   }
    }
  }
</style>
