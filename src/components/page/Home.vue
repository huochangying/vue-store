<template>
  <div class="home">
    <el-row>
      <el-col :span="8" class="store-order" id="order">
        <el-tabs class="box">
          <el-tab-pane label="点餐">
            <el-table :data="tableData">
              <el-table-column header-align="center" prop="name" label="商品名称"></el-table-column>
              <el-table-column header-align="center" prop="count" label="数量"></el-table-column>
              <el-table-column header-align="center" prop="price" label="金额"></el-table-column>
              <el-table-column header-align="center" label="操作">
                <template slot-scope="scope">
                  <el-button type="text" size="small" @click="deleteGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="result">
              <span>数量：{{totalCount}}</span>
              <span>金额：{{totalMoney}}</span>
            </div>
            <div class="cancel-btn">
              <el-button type="warning" size="small">挂单</el-button>
              <el-button type="danger" size="small" @click="deleteAll">删除</el-button>
              <el-button type="success" size="small" @click="checkOut">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">挂单</el-tab-pane>
          <el-tab-pane label="外卖">外卖</el-tab-pane>

        </el-tabs>

      </el-col>
      <el-col :span="16">
        <el-tabs class="box">
          <el-tab-pane label="常用商品">
            <ul class="goods-list">
              <li v-for="goods in allGoods" @click="addOrderList(goods)">
                <span>{{goods.goodsName}}</span>
                <span class="price">￥{{goods.price}}</span>
              </li>
            </ul>
          </el-tab-pane>
        </el-tabs>
        <el-tabs class="box">
          <el-tab-pane label="汉堡">
            <ul class="cookie-list">
              <li v-for="cookie in allCookie" @click="addOrderList(cookie)">
                <span class="cookieImg"><img :src="cookie.goodsImg"></span>
                <div>
                  <p>{{cookie.goodsName}}</p>
                  <p class="price">￥{{cookie.price}}</p>
                </div>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="小吃">
            <ul class="cookie-list">
              <li v-for="cookie in allCookieTwo" @click="addOrderList(cookie)">
                <span class="cookieImg"><img :src="cookie.goodsImg"></span>
                <div>
                  <p>{{cookie.goodsName}}</p>
                  <p class="price">￥{{cookie.price}}</p>
                </div>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="饮品">
            <ul class="cookie-list">
              <li v-for="cookie in allCookieThree" @click="addOrderList(cookie)">
                <span class="cookieImg"><img :src="cookie.goodsImg"></span>
                <div>
                  <p>{{cookie.goodsName}}</p>
                  <p class="price">￥{{cookie.price}}</p>
                </div>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="套餐">
            <ul class="cookie-list">
              <li v-for="cookie in allCookieFour" @click="addOrderList(cookie)">
                <span class="cookieImg"><img :src="cookie.goodsImg"></span>
                <div>
                  <p>{{cookie.goodsName}}</p>
                  <p class="price">￥{{cookie.price}}</p>
                </div>
              </li>
            </ul>
          </el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import ElRow from "element-ui/packages/row/src/row";
  import Axios from 'axios'

  export default {
    components: {ElRow},
    name: "home",
    data: () => ({
      totalCount: 0,
      totalMoney: 0,
      tableData: [],
      allGoods: [],
      allCookie: [],
      allCookieTwo: [],
      allCookieThree: [],
      allCookieFour: [],
    }),
    created: function () {
      Axios.get('http://jspang.com/DemoApi/oftenGoods.php')
        .then(response => {
          this.allGoods = response.data;
        })
        .catch(error => {
          console.log(error);
          alert('网络错误，不能访问');
        });
      Axios.get('http://jspang.com/DemoApi/typeGoods.php')
        .then(response => {
          this.allCookie = response.data[0];
          this.allCookieTwo = response.data[1];
          this.allCookieThree = response.data[2];
          this.allCookieFour = response.data[3];

        })
        .catch(error => {
          console.log(error);
          alert('网络错误，不能访问');
        })
    },
    mounted: function () {
      let orderHeight = document.body.clientHeight;
      document.querySelector('#order').style.height = orderHeight + "px"
    },
    methods: {
      addOrderList(goods) {
        this.totalCount = 0;
        this.totalMoney = 0;
        let _isHave = false;
        for (let i = 0; i < this.tableData.length; i++) {
          if (this.tableData[i].goodsId == goods.goodsId) {
            _isHave = true;
          }
        }

        if (_isHave) {
          let _arr = this.tableData.filter(x => x.goodsId == goods.goodsId);
          _arr[0].count++
        } else {
          let newGoods = {
            goodsId: goods.goodsId,
            name: goods.goodsName,
            price: goods.price,
            count: 1
          };
          this.tableData.push(newGoods);
        }

        this.resultCount();

      },
      deleteGoods(goods) {
        this.tableData = this.tableData.filter(x => x.goodsId != goods.goodsId);
        this.resultCount();
      },
      resultCount() {
        this.totalCount = 0;
        this.totalMoney = 0;
        if (this.tableData) {
          this.tableData.forEach((element) => {
            this.totalCount += element.count;
            this.totalMoney = this.totalMoney + (element.price * element.count);
          })
        }
      },
      deleteAll() {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
      },
      checkOut() {
        if (this.totalCount != 0) {
          this.tableData = [];
          this.totalCount = 0;
          this.totalMoney = 0;
          this.$message({
            message: '结账成功!',
            type: 'success'
          });
        } else {
          this.$message.error('您还没有购买任何商品！');
        }

      }
    }
  }
</script>

<style scoped>
  .store-order {
    background: #F9FAFC;
    border-right: 1px solid #C0CCDA;
  }

  .box {
    padding: 0 24px;
  }

  .cancel-btn {
    margin-top: 10px;
  }

  .goods-list li, .cookie-list li {
    padding: 5px 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    background: #fff;
    float: left;
    margin-right: 5px;
    margin-bottom: 5px;
    cursor: pointer;
  }

  .price {
    color: #1D8CE0;
  }

  .cookieImg {
    font-size: 0;
    display: inline-block;
  }

  .cookieImg img {
    width: 50px;
    height: 50px;
    border-radius: 5px;
    display: inline-block;
  }

  .cookie-list li span, .cookie-list li div {
    float: left;
  }

  .cookie-list li div {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 50px;
    padding-left: 5px;
  }

  .result {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 48px;
    background: #fff;
    border-bottom: 1px solid #ebeef5;
  }
</style>
