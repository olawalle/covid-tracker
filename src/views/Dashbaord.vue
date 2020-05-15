<!-- @format -->

<template>
  <div class="dashboard">
    <div class="map">
      lol
    </div>
    <div class="tables">
      <div class="top">
        <div class="count">
          <div class="smalls">
            Total Self-Assessed
          </div>
          <div class="no">
            1,234,524
          </div>
        </div>
        <div class="actions">
          <span class="country">
            Nigeria
          </span>
          <a-select style="width: 150px; height: 80px;" size="large"></a-select>
          <span class="blue"> <img src="../assets/printer.svg" alt="" /> Print </span>
        </div>
      </div>

      <div class="lists">
        <a-row :gutter="16">
          <a-col class="gutter-row" :sm="24" :md="8">
            <div class="gutter-box">
              <div class="desc">
                <div class="class">
                  HIGH RISK
                </div>
                <div class="population">
                  5,123
                </div>
                <div class="news">
                  969 New Cases
                </div>
              </div>
              <ul>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
              </ul>
            </div>
          </a-col>
          <a-col class="gutter-row" :sm="24" :md="8">
            <div class="gutter-box">
              <div class="desc">
                <div class="class">
                  HIGH RISK
                </div>
                <div class="population">
                  5,123
                </div>
                <div class="news">
                  969 New Cases
                </div>
              </div>
              <ul>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
              </ul>
            </div>
          </a-col>
          <a-col class="gutter-row" :sm="24" :md="8">
            <div class="gutter-box">
              <div class="desc">
                <div class="class">
                  HIGH RISK
                </div>
                <div class="population">
                  5,123
                </div>
                <div class="news">
                  969 New Cases
                </div>
              </div>
              <ul>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
                <li>
                  <P> <span>4,324</span> HIGH RISK </P>
                  Maryland, Lagos
                </li>
              </ul>
            </div>
          </a-col>
        </a-row>
      </div>

      <div class="mytable">
        <a-table :columns="columns" :dataSource="data" id="myTable" :pagination="{ pageSize: 25 }" :scroll="{ y: 200 }">
          <a @click="toAdminResult()" slot="name" slot-scope="text">{{ text }}</a>
        </a-table>
      </div>
    </div>
  </div>
</template>
<script>
  const columns = [
    {
      title: 'Name',
      dataIndex: 'name',
      key: 'name',
      scopedSlots: { customRender: 'name' },
      width: 100,
    },
    {
      title: 'Age',
      dataIndex: 'age',
      key: 'age',
      width: 50,
    },
    {
      title: 'Location',
      dataIndex: 'address',
      key: 'address',
      width: 130,
      ellipsis: true,
    },
    {
      title: 'Travel History',
      dataIndex: 'history',
      key: 'history',
      width: 100,
      ellipsis: true,
    },
    {
      title: 'Status',
      dataIndex: 'status',
      key: 'status',
      width: 50,
      ellipsis: true,
    },
  ]

  const data = [
    {
      key: '1',
      name: 'Jolayemi Modupe',
      age: 32,
      address: 'Maryland, Lagos.',
      history: 'Recent Traveller',
      status: 'HIGH',
    },
    {
      key: '2',
      name: 'Jolayemi Modupe',
      age: 32,
      address: 'Maryland, Lagos.',
      history: 'Recent Traveller',
      status: 'HIGH',
    },
    {
      key: '3',
      name: 'Jolayemi Modupe',
      age: 32,
      address: 'Maryland, Lagos.',
      history: 'Recent Traveller',
      status: 'HIGH',
    },
    {
      key: '4',
      name: 'Jolayemi Modupe',
      age: 32,
      address: 'Maryland, Lagos.',
      history: 'Recent Traveller',
      status: 'HIGH',
    },
    {
      key: '5',
      name: 'Jolayemi Modupe',
      age: 32,
      address: 'Maryland, Lagos.',
      history: 'Recent Traveller',
      status: 'HIGH',
    },
  ]
  export default {
    data() {
      return {
        data,
        columns,
      }
    },
    methods: {
      toAdminResult() {
        this.$router.push('/result/admin')
      },
    },
  }
</script>
<style lang="scss" scoped>
  .dashboard {
    .map {
      //   display: none;
      width: 50%;
      float: left;
      height: 100vh;
      background-color: #000;
    }
    .tables {
      width: 50%;
      float: left;
      background: #c4c4c438;
      height: 100vh;
      overflow: auto;
      .top {
        padding: 12px 10px;
        display: flow-root;
        background: #fff;
        .count {
          float: left;
          .smalls {
            font-size: 16px;
            line-height: 30px;
            letter-spacing: 0.005em;
            color: #413c3c;
            margin-bottom: 0;
          }
          .no {
            font-weight: bold;
            font-size: 36px;
            line-height: 67px;
            letter-spacing: 0.005em;
            margin-top: -15px;

            color: #413c3c;
          }
        }
        .actions {
          float: right;
          text-align: right;
          .country {
            border: 1px solid #0066ff;
            box-sizing: border-box;
            border-radius: 4px;
            padding: 12px 30px;
            margin-right: 12px;
          }
          .blue {
            color: #0066ff;
            padding-left: 20px;
            img {
              margin-right: 12px;
            }
          }
        }
      }
      .lists {
        display: block;
        padding: 15px;
        .gutter-row {
          height: 350px;
          .gutter-box {
            background-color: #fff;
            box-shadow: 0px 0px 1px rgba(0, 0, 0, 0.04), 0px 0px 2px rgba(0, 0, 0, 0.06), 0px 4px 8px rgba(0, 0, 0, 0.04);
            overflow: hidden;
            height: 350px;
            .desc {
              text-align: center;
              padding-top: 15px;
              height: 130px;
              background-color: #fff;
              .class {
                font-size: 16px;
                line-height: 27px;
                letter-spacing: 0.005em;

                color: #413c3c;
              }
              .population {
                font-weight: 600;
                font-size: 30px;
                line-height: 60px;
                letter-spacing: 0.005em;
                margin-top: -10px;

                color: #413c3c;
              }
              .news {
                font-size: 12px;
                line-height: 18px;
                letter-spacing: 0.005em;

                color: #413c3c;
                margin-top: -10px;
              }
            }
            ul {
              height: 220px;
              padding: 0;
              margin: 0;
              overflow: scroll;
              li {
                border-bottom: 2px solid #c4c4c438;
                padding: 10px;
                font-size: 14px;
                p {
                  margin-bottom: 4px;
                }
                span {
                  font-size: 16px;
                  font-weight: 500;
                  padding-right: 12px;
                }
              }
            }
          }
        }
      }
    }
    @media (max-width: 767px) {
      .map {
        width: 100%;
        height: auto;
        display: none;
      }
      .tables {
        width: 100%;
      }
      .gutter-row {
        margin-bottom: 12px;
      }
    }
  }
</style>
