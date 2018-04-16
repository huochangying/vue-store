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
                  <el-button type="text" size="small">删除</el-button>
                  <el-button type="text" size="small">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="cancel-btn">
              <el-button type="warning" size="small">挂单</el-button>
              <el-button type="danger" size="small">删除</el-button>
              <el-button type="success" size="small">结账</el-button>
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
              <li v-for="goods in allGoods">
                <span>{{goods.goodsName}}</span>
                <span class="price">￥{{goods.price}}</span>
              </li>
            </ul>
          </el-tab-pane>
        </el-tabs>
        <el-tabs class="box">
          <el-tab-pane label="汉堡">
            <ul class="cookie-list">
              <li v-for="cookie in allCookie">
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
              <li v-for="cookie in allCookieTwo">
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
              <li v-for="cookie in allCookieThree">
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
              <li v-for="cookie in allCookieFour">
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
      tableData: [{
        name: '可口可乐',
        price: 8,
        count: 1
      }, {
        name: '香辣鸡腿堡',
        price: 15,
        count: 1
      }, {
        name: '爱心薯条',
        price: 8,
        count: 1
      }, {
        name: '甜筒',
        price: 8,
        count: 1
      }],
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

</style>
