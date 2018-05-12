<template>
  <div id="app">

    <Row>
      <Col span="24">
        <h3 style="text-align: center;font-size: 2rem;border-bottom: 1px solid #666;">商城后台管理系统</h3>
      </Col>
    </Row>

    <Row style="height: 80vh;">
    <Col span="5" class="inner-container" style="max-height: 100%;overflow-y: auto;overflow-x: hidden;">
    <Menu :theme="'light'" :active-name="rp" :open-names="[rp]">

      <template v-for="(v,k) in navData">

        <Submenu :name="rp">

          <template slot="title">
            <Icon type="ios-paper"></Icon>
              {{v.title}}
          </template>

          <template v-for="(vv,kk) in v.item">
            <MenuItem :name="`/${vv.routeName}`" @click.native="routerPush(vv.navName)">{{vv.navName}}</MenuItem>
          </template>

        </Submenu>

      </template>
      
    </Menu>
    </Col>

    <Col span="19" style="overflow: hidden;">
      <router-view></router-view>
    </Col>

    </Row>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      rp: '',
      navData: [{
        title: '商品管理',
        item: [{
          navName: '轮播图',
          routeName: 'addSwipe'
        },{
          navName: '商品分类',
          routeName: 'goodsCla'
        },{
          navName: '添加/修改',
          routeName: 'addGoods'
        },{
          navName: '查看商品',
          routeName: 'GoodsList'
        }]
      },{
        title: '用户管理',
        item: [{
          navName: '用户列表',
          routeName: 'user'
        }]
      },{
        title: '买家秀',
        item: [{
          navName: '买家秀列表',
          routeName: 'aixiuList'
        }]
      },{
        title: '订单管理',
        item: [{
          navName: '全部订单',
          routeName: 'orderListAll'
        },{
          navName: '待付款',
          routeName: 'orderListNoPay'
        },{
          navName: '待发货',
          routeName: 'orderListPay'
        },{
          navName: '待收货',
          routeName: 'orderListWait'
        }]
      }]
    }
  },
  methods: {
    routerPush (vv) {
      switch(vv)
        {
        case '轮播图':
          this.$router.push({name:'addSwipe'})
          break;
        case '商品分类':
          this.$router.push({name:'goodsCla'})
          break;
        case '添加/修改':
          this.$router.push({name:'addGoods'})
          break;
        case '查看商品':
          this.$router.push({name:'GoodsList', params: {page: 0}})
          break;
        case '用户列表':
          this.$router.push({name:'user', params: {page: 0}})
          break;
        case '买家秀列表':
          this.$router.push({name:'aixiuList', params: {page: 0}})
          break;
        case '全部订单':
          this.$router.push({name:'orderListAll', params: {page: 0}, query: {orderStatus: 0}})
          break;
        case '待付款':
          this.$router.push({name:'orderListNoPay', params: {page: 0}, query: {orderStatus: 1}})
          break;
        case '待发货':
          this.$router.push({name:'orderListPay', params: {page: 0}, query: {orderStatus: 2}})
          break;
        case '待收货':
          this.$router.push({name:'orderListWait', params: {page: 0}, query: {orderStatus: 3}})
          break;
        default:
          console.log('default')
        }
    }
  },
  created: function () {
    let strIdx = this.$route.path.indexOf('/', 2)
    console.log(strIdx)
    if (strIdx !== -1) {
      this.rp = this.$route.path.slice(0, strIdx)
    } else {
      this.rp = this.$route.path
    }
    console.log(this.rp)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

 /* for Chrome */
.inner-container::-webkit-scrollbar {
    display: none;
}

/*.layout-copy{
    text-align: center;
    padding: 20px 0 20px;
    margin: 20px 0;
    color: #9ea7b4;
}*/
</style>
