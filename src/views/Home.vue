<template>
  <div class="home" id="home" name="home">
    <!-- 轮播图 -->
    <div class="block">
      <el-carousel height="460px">
        <el-carousel-item v-for="item in carousel" :key="item.carousel_id">
         <router-link :to="{ path: '/goods/details', query: {productID:item.product_id} }">
          <img style="height:460px;" :src="item.imgPath.includes('http')?item.imgPath:$target + item.imgPath" :alt="item.describes" />
            </router-link>
        </el-carousel-item>

      </el-carousel>
    </div>
    <!-- 轮播图END -->
    <div class="main-box">
      <div class="main">

        <!-- 欢乐甜品乐园 -->
        <div class="appliance" id="promo-menu">
          <div class="box-hd">
            <div class="title">欢乐甜品乐园</div>
            <div class="more" id="more">
              <MyMenu :val="4" @fromChild="getChildMsg1">
                <span slot="1">热门</span>
                <span slot="2">巧克力糖果区</span>
                <span slot="3">彩虹烘焙坊</span>
                <span slot="4">冰淇淋与饮品区</span>
              </MyMenu>
            </div>
          </div>
          <div class="box-bd">
            <div class="promo-list">
              <ul>
                <li>
                  <img v-lazy="imgUrl1" />
                </li>
                <li>
                  <img v-lazy="imgUrl2" />
                </li>
              </ul>
            </div>
            <div class="list">
              <MyList :list="applianceList1" :isMore="true"></MyList>
            </div>
          </div>
        </div>
        <!-- 欢乐甜品乐园END -->

        <!-- 魔力谷物能量站 -->
        <div class="appliance" id="promo-menu">
          <div class="box-hd">
            <div class="title">魔法谷物能量站</div>
            <div class="more" id="more">
              <MyMenu :val="4" @fromChild="getChildMsg">
                <span slot="1">热门</span>
                <span slot="2">膨化食品区</span>
                <span slot="3">坚果研磨所</span>
                <span slot="4">活力谷物唤醒站</span>
              </MyMenu>
            </div>
          </div>
          <div class="box-bd">
            <div class="promo-list">
              <ul>
                <li>
                  <img v-lazy="imgUrl3" />
                </li>
                <li>
                  <img v-lazy="imgUrl4" />
                </li>
              </ul>
            </div>
            <div class="list">
              <MyList :list="applianceList" :isMore="true"></MyList>
            </div>
          </div>
        </div>
        <!-- 魔力谷物能量站END -->

        <!-- 梦幻影院小食部 -->
        <div class="accessory" id="promo-menu">
          <div class="box-hd">
            <div class="title">梦幻影院小食部</div>
            <div class="more" id="more">
              <MyMenu :val="4" @fromChild="getChildMsg2">
                <span slot="1">热门</span>
                <span slot="2">果脯蜜饯阁</span>
                <span slot="3">炒货肉脯区</span>
                <span slot="4">包装零食区</span>
              </MyMenu>
            </div>
          </div>
          <div class="box-bd">
            <div class="promo-list">
              <ul>
                <li>
                  <img v-lazy="imgUrl5" alt />
                </li>
                <li>
                  <img v-lazy="imgUrl6" alt />
                </li>
              </ul>
            </div>
            <div class="list">
              <MyList :list="accessoryList" :isMore="true"></MyList>
            </div>
          </div>
        </div>
        <!-- 梦幻影院小食部END -->
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      carousel: "", // 轮播图数据
      phoneList: "", // 手机商品列表
      miTvList: "", // Mickey电视商品列

      applianceList1: "", // 甜品区列表
      applianceHotList1: "", //热门甜品商品列表
      Chocolate_candy_list: "",
      Rainbow_Bakery:"" ,
      Ice_cream_and_drinks_list:"",

      applianceList: "", // 谷物区列表
      applianceHotList: "", //热门谷物商品列表
      Puffed_food_List:"",
      Potato_chip_Nut:"",
      Vitality_cereal_wake_up_list:"",

      accessoryList: "", //梦幻影院小食部商品列表
      accessoryHotList: "", //热门小食商品列表
      Preserve_fruit_list:"",
      fried_meat_breast_list:"",
      packing_snack_list:"",


      protectingShellList: "", // 保护套商品列表
      chargerList: "", //充电器商品列表

      applianceActive: 1, // 谷物当前选中的商品分类
      applianceActive1: 1, // 甜品当前选中的商品分类
      accessoryActive: 1, // 小食当前选中的商品分类

      imgUrl1: "http://localhost:3000/admin/show_images/9bf44e32-1179-49c7-ae78-ee7e2c6b6c3b.png",
      imgUrl2: "http://localhost:3000/admin/show_images/7ec506bd-b03e-4480-ac46-6ea604e56e22.png",
      imgUrl3: "http://localhost:3000/admin/show_images/3edd4116-4ffa-4c20-ba29-8bab58dbc397.png",
      imgUrl4: "http://localhost:3000/admin/show_images/97b73009-9ff1-4b9b-b199-561ddd0c1ec9.png",
      imgUrl5: "http://localhost:3000/admin/show_images/ae442645-a810-46aa-a023-ce60ab085515.png",
      imgUrl6: "http://localhost:3000/admin/show_images/16c9946c-9a88-4b45-8ea1-fbec5294b618.png",
    };
  },
  watch: {
    //甜品
    applianceActive1: function(val) {
      // 页面初始化的时候把applianceHotList(热门家电商品列表)直接赋值给applianceList(家电商品列表)
      // 所以在切换商品列表时判断applianceHotList是否为空,为空则是第一次切换,把applianceList赋值给applianceHotList
      if (this.applianceHotList1 == "") {
        this.applianceHotList1 = this.applianceList1;
        console.log("甜品区的热门："+this.applianceHotList1)
      }
      if (val == 1) {
        // 1为热门商品
        this.applianceList1 = this.applianceHotList1;
        return;
      }
      if (val == 2) {
        // 2为巧克力糖果区
        this.applianceList1 = this.Chocolate_candy_list;
        return;
      }
      if (val == 3) {
        // 彩虹烘焙坊
        this.applianceList1 = this.Rainbow_Bakery;
        return;
      }
      if (val == 4) {
        // 冰淇淋与饮品区
        this.applianceList1 = this.Ice_cream_and_drinks_list;
        return;
      }
    },
    // 家电当前选中的商品分类，响应不同的商品数据
    applianceActive: function(val) {
      // 页面初始化的时候把applianceHotList(热门家电商品列表)直接赋值给applianceList(家电商品列表)
      // 所以在切换商品列表时判断applianceHotList是否为空,为空则是第一次切换,把applianceList赋值给applianceHotList
      if (this.applianceHotList == "") {
        this.applianceHotList = this.applianceList;
      }
      if (val == 1) {
        // 1为热门商品
        this.applianceList = this.applianceHotList;
        return;
      }
      if (val == 2) {
        // 膨化食品区
        this.applianceList = this.Puffed_food_List;
        return;
      }
      if (val == 3) {
        // 坚果研磨所
        this.applianceList = this.Potato_chip_Nut;
        console.log("===坚果研磨所的applianceList===")
        console.log(this.applianceList)
        return;
      }
      if (val == 4) {
        // 活力谷物唤醒站
        this.applianceList = this.Vitality_cereal_wake_up_list;
        return;
      }

    },
    accessoryActive: function(val) {
      // 页面初始化的时候把accessoryHotList(热门配件商品列表)直接赋值给accessoryList(配件商品列表)
      // 所以在切换商品列表时判断accessoryHotList是否为空,为空则是第一次切换,把accessoryList赋值给accessoryHotList
      if (this.accessoryHotList == "") {
        this.accessoryHotList = this.accessoryList;
      }
      if (val == 1) {
        // 1为热门商品
        this.accessoryList = this.accessoryHotList;
        return;
      }
      if (val == 2) {
        // 果脯蜜饯阁
        this.accessoryList = this.Preserve_fruit_list;
        return;
      }
      if (val == 3) {
        //3 炒货肉脯区
        this.accessoryList = this.fried_meat_breast_list;
        return;
      }
      if (val == 4) {
        //包装零食区
        this.accessoryList = this.packing_snack_list;
        return;
      }
    }
  },
  created() {
    // 获取轮播图数据
    this.$axios
      .post("/api/carousel/list", {})
      .then(res => {
        this.carousel = res.data.data;
      })
      .catch(err => {
        return Promise.reject(err);
      });
    // 获取各类商品数据
    this.getPromo("冰淇淋与饮品区", "Ice_cream_and_drinks_list");
    this.getPromo("彩虹烘焙坊", "Rainbow_Bakery");
    this.getPromo("巧克力糖果区", "Chocolate_candy_list");
    this.getPromo("坚果研磨所", "Potato_chip_Nut");
    this.getPromo("膨化食品区", "Puffed_food_List");
    this.getPromo("活力谷物唤醒站", "Vitality_cereal_wake_up_list");
    this.getPromo("果脯蜜饯阁", "Preserve_fruit_list");
    this.getPromo("炒货肉脯区", "fried_meat_breast_list");
    this.getPromo("包装零食区", "packing_snack_list");
    this.getPromo(
        ["巧克力糖果区", "彩虹烘焙坊", "冰淇淋与饮品区"],
        "applianceList1",
        "/api/product/hots"
    );
    this.getPromo(
      ["膨化食品区", "坚果研磨所", "活力谷物唤醒站"],
      "applianceList",
      "/api/product/hots"
    );
    this.getPromo(
      ["果脯蜜饯阁", "炒货肉脯区", "包装零食区"],
      "accessoryList",
      "/api/product/hots"
    );
  },
  methods: {

    getChildMsg1(val) {
      this.applianceActive1 = val;
    },
    // 获取家电模块子组件传过来的数据
    getChildMsg(val) {
      this.applianceActive = val;
    },
    // 获取配件模块子组件传过来的数据
    getChildMsg2(val) {
      this.accessoryActive = val;
    },
    // 获取各类商品数据方法封装
    getPromo(categoryName, val, api) {
      api = api != undefined ? api : "/api/product/promo";
      this.$axios
        .post(api, {
          categoryName
        })
        .then(res => {
          this[val] = res.data.data;
        })
        .catch(err => {
          return Promise.reject(err);
        });
    }
  }
};
</script>
<style scoped>
@import "../assets/css/index.css";
</style>