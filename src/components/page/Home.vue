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
                  <p >{{cookie.goodsName}}</p>
                  <p  class="price">￥{{cookie.price}}</p>
                </div>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="小吃"></el-tab-pane>
          <el-tab-pane label="饮品"></el-tab-pane>
          <el-tab-pane label="套餐"></el-tab-pane>
        </el-tabs>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import ElRow from "element-ui/packages/row/src/row";

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
      allGoods: [
        {
          goodsId: 1,
          goodsName: '香辣鸡腿堡',
          price: 18
        }, {
          goodsId: 2,
          goodsName: '田园鸡腿堡',
          price: 15
        }, {
          goodsId: 3,
          goodsName: '和风汉堡',
          price: 15
        }, {
          goodsId: 4,
          goodsName: '快乐全家桶',
          price: 80
        }, {
          goodsId: 5,
          goodsName: '脆皮炸鸡腿',
          price: 10
        }, {
          goodsId: 6,
          goodsName: '魔法鸡块',
          price: 20
        }, {
          goodsId: 7,
          goodsName: '可乐大杯',
          price: 10
        }, {
          goodsId: 8,
          goodsName: '雪顶咖啡',
          price: 18
        }, {
          goodsId: 9,
          goodsName: '大块鸡米花',
          price: 15
        }, {
          goodsId: 20,
          goodsName: '香脆鸡柳',
          price: 17
        }
      ],
      allCookie: [
        {
          goodsId: 1,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
          goodsName: '香辣鸡腿堡',
          price: 18
        }, {
          goodsId: 2,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
          goodsName: '田园鸡腿堡',
          price: 15
        }, {
          goodsId: 3,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: '和风汉堡',
          price: 15
        }, {
          goodsId: 4,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: '快乐全家桶',
          price: 80
        }, {
          goodsId: 5,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: '脆皮炸鸡腿',
          price: 10
        }, {
          goodsId: 6,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
          goodsName: '魔法鸡块',
          price: 20
        }, {
          goodsId: 7,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
          goodsName: '可乐大杯',
          price: 10
        }, {
          goodsId: 8,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
          goodsName: '雪顶咖啡',
          price: 18
        }, {
          goodsId: 9,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
          goodsName: '大块鸡米花',
          price: 15
        }, {
          goodsId: 20,
          goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
          goodsName: '香脆鸡柳',
          price: 17
        }
      ],
    }),
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
  .cookie-list li div{
    display: flex;
    flex-direction:column;
    justify-content: center;
    align-items: center;
    height: 50px;
    padding-left: 5px;
  }

</style>
