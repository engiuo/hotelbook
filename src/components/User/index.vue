<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Open+Sans:wght@400;700&display=swap"></link>
<template>
    <el-container>
  <el-header><el-menu
  :default-active="activeIndex2"
  class="el-menu-demo centered-menu"
  mode="horizontal"
  @select="handleSelect"
  background-color="#545c64"
  text-color="#fff"
  active-text-color="#ffd04b">
  <el-menu-item index="1">关于我们</el-menu-item>
  <el-submenu index="2">
    <template slot="title">客户服务</template>
    <el-menu-item index="2-1" @click="handleBook">房间预订</el-menu-item>
    <el-menu-item index="2-3-1" @click="handleMeal">餐饮预订</el-menu-item>
    <el-menu-item index="2-2"><a href="https://www.ele.me" target="_blank">外卖合作商-饿了么外卖</a></el-menu-item>
    <el-submenu index="2-3">
      <template slot="title">设施预订</template>
      
      <el-menu-item index="2-3-2" @click="handlehot"> 温泉预约</el-menu-item>
      <el-menu-item index="2-3-3" @click="handleGym"> 健身房预约</el-menu-item>
      <el-menu-item index="2-3-4" @click="handlePool"> 游泳馆预约</el-menu-item>
    </el-submenu>
  </el-submenu>
  <el-submenu index="3">
    <template slot="title">当前用户：{{username}}</template>
    <el-menu-item index="3" @click="handleCenter">会员中心</el-menu-item>
  <el-menu-item index="3" @click="handleLogin">登录</el-menu-item>
  <el-menu-item index="4" @click="handleRegister">注册</el-menu-item>
  <el-menu-item index="6" @click="handleOut">登出</el-menu-item>
  </el-submenu>
      </el-menu>

  </el-header>
  <el-main>
    <div class="carousel-container"></div>
    <el-carousel interval="3000" height="850px" direction="vertical" :autoplay="true" @change="handleCarouselChange">
      <el-carousel-item v-for="item in carouselItems" :key="item.id">
      <el-image :src="item.image" style="width: 100%; height: 100%;" fit="cover"></el-image>
      
    </el-carousel-item>
        </el-carousel><div class="carousel-text">
            <div class="title">{{ currentCarouselItem.title }}</div>
                                <div class="description">{{ currentCarouselItem.description }}</div>
        </div>
    </el-main>
    <el-button type="primary" @click="handleBook">立即预定创新港大酒店</el-button>
    <el-divider><i class="el-icon-s-home" ></i></el-divider>
<span>客房特色</span>
<el-carousel :interval="4000" type="card" height="500px" :autoplay="true" @change="handleCarouselChange">
  <el-carousel-item v-for="item in carouselItemss" :key="item.ida">
      <el-image :src="item.image" style="width: 100%; height: 100%;" fit="cover"></el-image>
      
    </el-carousel-item>
  </el-carousel>
</el-container>

  </template>
  <script>
  export default {
    handleCarouselChange(index) {
    },
    mounted() {
    // 设置初始值
    console.log('currentCarouselItem:', this.currentCarouselItem);
    if(this.user != null){
      this.username = this.user.userName;
    }
  },
    data() {
      return {
        user: JSON.parse(localStorage.getItem('user')),
        username: '未登录',
        show2: true,
        activeIndex: '1',
        activeIndex2: '1',
        carouselItems: [
        { id: 1, image:require('@/assets/jieshao1.png' ) },
        { id: 2, image:require('@/assets/jieshao2.jpg' )},
        { id: 3, image:require('@/assets/shouye3.jpeg' )},
        
      ],
      carouselItemss: [
        { ida: 1, image:require('@/assets/room1.png' ) },
        { ida: 2, image:require('@/assets/room2.png' )},
        { ida: 3, image:require('@/assets/room3.png' )},
        { ida: 4, image:require('@/assets/room4.png' ) },
        { ida: 5, image:require('@/assets/room5.png' )},
        { ida: 6, image:require('@/assets/room6.png' ) },
        { ida: 7, image:require('@/assets/room7.png' )},
      ],
      currentCarouselItem: { title: '创新港大酒店', description: '西安交通大学旗下高端酒店品牌，源于陕西，秉承百年匠心精神，打造精致的酒店产品和服务；创新港大酒店在尊重传统的同时，用新的视角重塑现代化的西北经典服务。' }
      };
    },
    methods: {
      handleSelect(key, keyPath) {
        console.log(key, keyPath);
      },
      handleCenter() {
        if(this.user.userIsvip==0){
          this.$router.push("/admin/index");
        }
        else{
          this.$router.push("/my");
        }
    },
      handleLogin() {
        this.$router.push("/login");
    },
    handleRegister(){
      this.$router.push("/register");
    },
    handleOut(){
      localStorage.removeItem("user");
      location.reload();
    },
    handleBook() {
      if(this.user==null){
        this.$message({
          message: '请先登录',
          type: 'warning'
        });
        this.$router.push("/login");
      }else{
      this.$router.push("/book");}
    },
    handleMeal() {
      if(this.user==null){
        this.$message({
          message: '请先登录',
          type: 'warning'
        });
        this.$router.push("/login");
      }else{
      this.$router.push("/bookmeal");}
    },handlePool() {
      if(this.user==null){
        this.$message({
          message: '请先登录',
          type: 'warning'
        });
        this.$router.push("/login");
      }else{
      this.$router.push("/Pool");
      }
    },handlehot() {
      if(this.user==null){
        this.$message({
          message: '请先登录',
          type: 'warning'
        });
        this.$router.push("/login");
      }else{
      this.$router.push("/hot");}
    },handleGym() {
      if(this.user==null){
        this.$message({
          message: '请先登录',
          type: 'warning'
        });
        this.$router.push("/login");
      }
      else{
      this.$router.push("/Gym");
      }
    },
    handleCarouselChange(index) {
      // 这里不再更新currentCarouselItem，保持全局文字部分不随轮播项变化
    }
    }
  }
</script>
  <style>
  .carousel-container {
  position: relative;
}
  .carousel-text {
  position: relative;
  bottom: 500px; /* 调整文字的垂直位置 */
  left: 50%; /* 居中 */
  transform: translateX(-50%);
  color: #060606; /* 文字颜色 */
  text-align: center;
  z-index: 10; /* 设置一个较高的 z-index */
  margin-bottom: -450px; /* 调整文字与轮播图之间的间距 */
  /* 其他样式可以根据需要添加 */
}

.title {
  font-size: 100px; /* 标题文字大小 */
  margin-bottom: 270px; /* 调整标题与介绍之间的间距 */
  font-family: 'Dancing Script', cursive;
  color: #ffffff; /* 设置标题颜色为深蓝色 */
  font-weight: bolder; /* 设置标题为粗体 */
}

.description {
  font-size: 30px; /* 介绍文字大小 */
  font-family: "Times New Roman", Times, serif;
  color: #ffffff; /* 设置描述颜色为深灰色 */
  font-weight: bold; /* 设置描述为普通（非粗体） */
}
  .transition-box {
    margin-bottom: 10px;
    width: 200px;
    height: 100px;
    border-radius: 4px;
    background-color: #409EFF;
    text-align: center;
    color: #fff;
    padding: 40px 20px;
    box-sizing: border-box;
    margin-right: 20px;
  }
  .el-carousel__item h3 {
    color: #475669;
    font-size: 14px;
    opacity: 0.75;
    line-height: 200px;
    margin: 0;
  }
  
  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
    .el-carousel__item h3 {
      color: #475669;
      font-size: 14px;
      opacity: 0.75;
      line-height: 200px;
      margin: 0;
    }
    
    .el-carousel__item:nth-child(2n) {
      background-color: #99a9bf;
    }
    
    .el-carousel__item:nth-child(2n+1) {
      background-color: #d3dce6;
    }
    .centered-menu {
    display: flex;
    justify-content: center;
  }
  .right-aligned-menu {
    display: flex;
    justify-content: flex-end;
  }
  .right-buttons {
    margin-left: auto; /* 将右侧按钮容器推到最右侧 */
    display: flex;
    align-items: center;
  }
  </style>