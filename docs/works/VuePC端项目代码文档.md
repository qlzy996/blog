# VuePC端项目代码文档

## main.js

```js
import Vue from 'vue'
import App from './App.vue'
import './permission' // 引用权限模块
import router from './router'
import ElementUI from 'element-ui' // 引入模块
import Component from './components'
import 'element-ui/lib/theme-chalk/index.css' // 引入样式
import './styles/index.less' // 引入初始化样式
import axios from './utils/request'
Vue.prototype.$axios = axios // 赋值给全局对象
Vue.use(ElementUI) // 全局注册
Vue.use(Component) // 全局注册
Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

## APP.vue

```html
<template>
  <!-- 一级路由容器 -->
  <router-view/>
</template>

<style lang="less">

</style>
```

## views

### account

```html
<template>
  <el-card v-loading="loading">
      <bread-crumb slot="header">
        <template slot='title'>账户信息</template>
      </bread-crumb>
      <!-- 表单 => 表单容器 -->
      <el-form ref="myForm" :model="formData" :rules="rules" style="margin-left:100px" label-width="100px">
          <el-form-item prop="name" label="用户名">
              <el-input v-model="formData.name" style="width:40%"></el-input>
          </el-form-item>
           <el-form-item  label="简介">
               <el-input v-model="formData.intro" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item prop="email" label="邮箱">
               <el-input v-model="formData.email" style="width:40%"></el-input>
           </el-form-item>
           <el-form-item label="手机号">
               <el-input v-model="formData.mobile" disabled style="width:40%"></el-input>
           </el-form-item>
           <el-form-item>
               <el-button @click="saveUserInfo" type="primary">保存信息</el-button>
           </el-form-item>
      </el-form>
      <!-- 上传组件 -->
      <el-upload :http-request="uploadImg" class='head-upload' action="" :show-file-list="false">
          <img :src="formData.photo ? formData.photo : defaultImg" alt="">
      </el-upload>
  </el-card>
</template>

<script>
import eventBus from '../../utils/eventBus'
export default {
  data () {
    return {
      loading: false,
      formData: {
        name: '', // 用户名
        intro: '', // 简介
        photo: '', // 头像
        email: '', // 邮箱
        mobile: ''
      },
      defaultImg: require('../../assets/img/cat.jpg'),
      rules: {
        //   用户名 邮箱
        name: [{ required: true, message: '用户名不能为空' }, {
          min: 1, max: 7, message: '用户名长度在1到7个字符'
        }],
        email: [{ required: true, message: '邮箱不能为空' }, {
          pattern: /^([a-zA-Z]|[0-9])(\w|-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/,
          message: '邮箱格式不正确'
        }]

      }
    }
  },
  methods: {
    uploadImg (params) {
      this.loading = true // 打开弹层
      let data = new FormData()
      data.append('photo', params.file)
      this.$axios({
        url: '/user/photo',
        method: 'patch',
        data
      }).then(result => {
        this.loading = false // 关闭弹层
        this.formData.photo = result.data.photo // 给当前的头像赋值
        // 认为保存成功 => 通知header组件 更新信息
        eventBus.$emit('updateUserInfo')
      })
    },
    //   获取用户个人信息
    getUserInfo () {
      this.$axios({
        url: '/user/profile'
      }).then(result => {
        this.formData = result.data
      })
    },
    // suncaiGuanli  => 千万杜绝
    // baocunyonghuxinxi
    // 保存用户信息
    saveUserInfo () {
      this.$refs.myForm.validate().then(result => {
        //  调用保存接口
        this.$axios({
          url: '/user/profile',
          method: 'patch',
          data: this.formData
        }).then(result => {
          this.$message({
            type: 'success',
            message: '保存用户信息成功'
          })
          // 认为保存成功 => 通知header组件 更新信息
          eventBus.$emit('updateUserInfo')
        })
      })
    }
  },
  created () {
    this.getUserInfo()
  }

}
</script>

<style lang='less' scoped>
   .head-upload {
      position: absolute;
      right: 300px;
      top:200px;
       img {
          width: 200px;
          height: 200px;
           border-radius: 50%;
       }
   }
</style>

```

### articles

```html
<template>
  <el-card class='articles'>
      <bread-crumb slot='header'>
         <template slot='title'>文章列表</template>
      </bread-crumb>
      <!-- 表单容器 -->
      <el-form style="padding-left:50px">
          <el-form-item label="文章状态:">
              <!-- 放置一个单选组  文章状态，0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除，不传为全部-->
              <!-- 第一种 用监听组件的形式去做搜索 -->
                 <!-- <el-radio-group v-model="searchForm.status" @change="changeCondition">
                  <el-radio :label="5">全部</el-radio>
                  <el-radio :label="0">草稿</el-radio>
                  <el-radio :label="1">待审核</el-radio>
                  <el-radio :label="2">审核通过</el-radio>
                  <el-radio :label="3">审核失败</el-radio>
              </el-radio-group> -->
              <el-radio-group v-model="searchForm.status" >
                  <!-- label -->
                  <el-radio :label="5">全部</el-radio>
                  <el-radio :label="0">草稿</el-radio>
                  <el-radio :label="1">待审核</el-radio>
                  <el-radio :label="2">审核通过</el-radio>
                  <el-radio :label="3">审核失败</el-radio>
              </el-radio-group>
          </el-form-item>
          <el-form-item label="频道列表:">
              <!-- 第一种 用监听组件的形式去做搜索 -->
               <!-- <el-select @change="changeCondition" placeholder="请选择频道" v-model="searchForm.channel_id">
                  <el-option v-for="item in channels" :key="item.id" :label="item.name" :value="item.id"></el-option>
              </el-select> -->
              <el-select placeholder="请选择频道" v-model="searchForm.channel_id">
                  <!-- el-option label是显示值 value是存储值 -->
                  <el-option v-for="item in channels" :key="item.id" :label="item.name" :value="item.id"></el-option>
              </el-select>
          </el-form-item>
          <el-form-item label="时间选择:">
              <!-- 日期选择器 日期范围-->
              <!-- 第一种 用监听组件的形式去做搜索 -->
            <!-- <el-date-picker @change="changeCondition" value-format="yyyy-MM-dd" v-model="searchForm.dateRange" type="daterange"></el-date-picker> -->
              <el-date-picker  value-format="yyyy-MM-dd" v-model="searchForm.dateRange" type="daterange"></el-date-picker>
          </el-form-item>
      </el-form>
      <el-row class='total' type='flex' align="middle">
          <span>
              共找到{{page.total}}条符合条件的内容
          </span>
      </el-row>
      <div class='article-item' v-for="item in list" :key="item.id.toString()">
          <!-- 左侧 -->
          <div class='left'>
              <img :src="item.cover.images.length ? item.cover.images[0] : defaultImg" alt="">
              <div class='info'>
                  <span>{{ item.title }}</span>
                  <!-- 文章状态 0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除 -->
                  <el-tag :type="item.status | filterType" class='tag'>{{ item.status | filterStatus }}</el-tag>
                  <span class='date'>{{ item.pubdate }}</span>
              </div>
          </div>
          <!-- 右侧 -->
          <div class='right'>
              <span @click="toModify(item.id)"><i class="el-icon-edit"></i>修改</span>
              <!-- 注册删除按钮事件 -->
              <span @click="delMaterial(item.id)"><i class="el-icon-delete"></i>删除</span>
          </div>
      </div>
      <el-row type='flex' justify="center" align="middle" style="height:60px">
          <el-pagination  background layout="prev, pager, next"
          :total="page.total"
          :current-page="page.currentPage"
          :page-size="page.pageSize"
          @current-change="changePage"
          ></el-pagination>
      </el-row>
  </el-card>
</template>

<script>
/******
 * author gaoly
 * created by 2019-12-21
 * modify  by liun
 * ********/
import { getArticles, getChannels } from '../../actions/articles'
export default {
  data () {
    return {
      searchForm: {
        status: 5, // 默认应该选中全部
        channel_id: null, // 默认不选中任何一个分类
        dateRange: [] // 日期范围
      },
      channels: [], // 接收频道数据
      list: [],
      defaultImg: require('../../assets/img/default.jpg'), // 默认图片
      page: {
        currentPage: 1,
        pageSize: 10, // 黑马头条后端限制 最低10条 => 文章列表
        total: 0
      }
    }
  },
  watch: {
    searchForm: {
      handler: function () {
        // 此时数据已经变成最新的了
        // this 指向组件实例
        this.changeCondition() // 直接调用条件改变的方法
      },
      deep: true
    }
  },
  filters: {
    //   过滤器第一个参数 是value
    filterStatus (value) {
      //  文章状态 0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除
      switch (value) {
        case 0:
          return '草稿'
        case 1:
          return '待审核'
        case 2:
          return '已发表'
        case 3:
          return '审核失败'
        default:
          break
      }
    },
    filterType (value) {
      //  文章状态 0-草稿，1-待审核，2-审核通过，3-审核失败，4-已删除
      switch (value) {
        case 0:
          return 'warning'
        case 1:
          return 'info'
        case 2:
          return ''
        case 3:
          return 'danger'
        default:
          break
      }
    }
  },
  methods: {
    // 去修改页面 => 实际上就是发布页面
    toModify (id) {
      this.$router.push(`/home/publish/${id.toString()}`)
    },
    // 删除文章
    async delMaterial (id) {
      await this.$confirm('是否要删除该文章?')
      // 调用删除接口
      await this.$axios({
        method: 'delete',
        url: `/articles/${id.toString()}`
      })
      // 提示
      this.$message({
        type: 'success',
        message: '删除成功'
      })
      // 重新拉取数据
      // this.page.currentPage = 1 // 根据业务 处理 如果删除了数据 是否回到第一页根据具体业务而定
      this.getConditionArticle()
    },
    //   改变页码方法
    changePage (newPage) {
      this.page.currentPage = newPage // 最新页码
      this.getConditionArticle() // 调用获取文章数据
    },
    //   改变条件
    changeCondition () {
      this.page.currentPage = 1 // 强制将页码重置第一页
      this.getConditionArticle() // 调用获取文章数据
    },
    getConditionArticle () {
      debugger
      let params = {
        page: this.page.currentPage,
        per_page: this.page.pageSize,
        status: this.searchForm.status === 5 ? null : this.searchForm.status, // 因为5是前端定义的一个标识, 如果等于5 表示查全部, 全部应该什么都不传 直接传null
        channel_id: this.searchForm.channel_id,
        begin_pubdate: this.searchForm.dateRange && this.searchForm.dateRange.length ? this.searchForm.dateRange[0] : null, // 开始时间
        end_pubdate: this.searchForm.dateRange && this.searchForm.dateRange.length > 1 ? this.searchForm.dateRange[1] : null // 截止时间
      }
      // 加上一个非空处理
      this.getArticles(params)
    },
    //   获取所有的频道
    async getChannels () {
      let result = await getChannels()
      this.channels = result.data.channels
    },
    // 获取文章列表数据
    async  getArticles (params) {
      let result = await getArticles() // 调用获取文章模块
      this.list = result.data.results // 获取文章列表数据
      this.page.total = result.data.total_count // 总数
    }
  },
  created () {
    this.getChannels() // 获取文章数据
    this.getArticles({ page: 1, per_page: 10 }) // 获取文章列表数据
  }
}
</script>

<style lang='less' scoped>
  .articles {
      .total {
          height: 60px;
          border-bottom: 1px dashed #ccc;
      }
      .article-item {
          display: flex;
          justify-content: space-between;
          padding: 20px 0;
          border-bottom: 1px solid #f2f3f5;
          .left {
              display: flex;
              img {
                  width: 180px;
                  height: 100px;
                  border-radius: 4px;
              }
              .info {
                  height: 100px;
                  margin-left: 10px;
                  display: flex;
                  flex-direction: column;
                  justify-content: space-around;
                  .date {
                      color: #999;
                      font-size:12px;
                  }
                  .tag {
                      text-align: center;
                      width:60px;
                  }
              }
          }
          .right {
              span {
                  font-size:14px;
                  margin-right: 8px;
                  cursor: pointer;
              }
          }
      }
  }
</style>

```



### comment

```html
<template>
  <!-- 卡片组件 -->
  <el-card  v-loading="loading">
    <bread-crumb slot="header">
      <!-- 插槽内容 -->
      <template slot="title">评论管理</template>
    </bread-crumb>
    <!-- el-table -->
    <!-- 表格 -->
    <el-table :data="list">
      <!-- 放置列组件 width宽度 label表头 prop 字段名 -->
      <el-table-column prop="title" width="600" label="标题"></el-table-column>
      <el-table-column :formatter="formatterBoolean" prop="comment_status" label="评论状态"></el-table-column>
      <el-table-column prop="total_comment_count" label="总评论数"></el-table-column>
      <el-table-column prop="fans_comment_count" label="粉丝评论数"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="obj">
          <!-- 作用域插槽 -->
          <el-button size="small" type="text">修改</el-button>
          <!-- 需要根据状态来进行判断是关闭还是打开 -->
          <el-button
            @click="openOrCloseState(obj.row)"
            size="small"
            type="text"
          >{{ obj.row.comment_status ? '关闭' : '打开' }}评论</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-row type='flex' justify="center" align="middle" style="height:80px">
      <!-- 分页组件 total 总页码  每页多少条-->
      <el-pagination background layout="prev, pager, next"
       :current-page="page.currentPage"
       :page-size="page.pageSize"
       :total="page.total"
       @current-change="changePage"
       ></el-pagination>
    </el-row>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      list: [], // 定义一个数据接收返回结果
      loading: false, // 默认不打开进度条
      page: {
        total: 0,
        pageSize: 10, // 默认每页条数为10
        currentPage: 1 // 默认页码为1
      } // 专门存放分页信息数据
    }
  },
  methods: {
    // 页码改变事件
    changePage (newPage) {
      this.page.currentPage = newPage // 最新的页码
      this.getComment()
    },
    async getComment () {
      this.loading = true // 打开进度条
      let result = await this.$axios({
        url: '/articles',
        params: { response_type: 'comment', page: this.page.currentPage, per_page: this.page.pageSize }
      })
      this.list = result.data.results
      this.page.total = result.data.total_count // 总条数
      this.loading = false
    },
    // 定义一个格式化的函数
    formatterBoolean (row, column, cellValue, index) {
      // row => 当前行数据
      // column => 当前列信息
      // celllValue => 当前的单元格的值
      // index 索引
      return cellValue ? '正常' : '关闭'
    },
    // 打开或者关闭评论
    async openOrCloseState (row) {
      // 直接调用接口
      let mess = row.comment_status ? '关闭' : '打开'
      try {
        await this.$confirm(`您是否确定要${mess}评论吗`, '提示')
        await this.$axios({
          method: 'put',
          url: '/comments/status',
          params: { article_id: row.id.toString() },
          data: { allow_comment: !row.comment_status } // 因为当前如果是打开 ,就要关闭 如果是关闭 就要打开
        })
        this.getComment() // 重新拉取评论管理数据
      } catch (error) {

      }
    }
  },
  created () {
    this.getComment() // 获取数据
  }
}
</script>

<style>
</style>

```

### home

#### home.vue

```html
<template>
 <el-carousel height="500px" type="card" :interval="5000" arrow="always">
    <el-carousel-item  v-for="item in list" :key="item">
      <img :src="item" alt="">
    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  data () {
    return {
      list: ['http://gss0.baidu.com/7Po3dSag_xI4khGko9WTAnF6hhy/zhidao/pic/item/b21c8701a18b87d608167af6050828381e30fd87.jpg', 'http://file.mumayi.com/forum/201401/16/202014h22z6jt6vpajypd0.jpg', 'http://g.hiphotos.baidu.com/zhidao/pic/item/fd039245d688d43f499c5b3e7f1ed21b0ff43bc1.jpg']
    }
  }
}
</script>

<style>

  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
</style>

```



#### index.vue

```html
<template>
  <!-- 放置一个大容器 -->
  <el-container>
    <!-- 左右布局 -->
    <el-aside :style="{width: collapse ? '60px' : '230px'}" style="transition: all 0.5s;  min-height:100vh;background-color:#353b4e;">
      <layout-aside :collapse="collapse"></layout-aside>
    </el-aside>
    <!-- 右侧容器 -->
    <el-container>
      <!-- 上下布局 -->
      <el-header>
        <!-- 头部组件 -->
        <layout-header></layout-header>
      </el-header>
      <el-main>
         <!-- 二级路由容器 -->
         <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import eventBus from '../../utils/eventBus'
export default {
  data () {
    return {
      collapse: false // 默认是展开
    }
  },
  created () {
    // 开启监听
    eventBus.$on('changeCollapse', () => {
      // 头部组件告诉折叠相关的所有组件 要改变了
      this.collapse = !this.collapse
    })
  }
}
</script>

<style>

</style>

```



### login

```html
<template>
  <div class="login">
    <!-- 放置一个el-card组件 -->
    <el-card class='login-card'>
      <!-- 放置标题图片 -->
      <div class='title'>
        <img src="../../assets/img/logo_index.png" alt="">
      </div>
      <!-- 放置表单  el-form model  绑定数据对象 -->
      <el-form ref="myForm" :model="loginForm" :rules="loginRules">
        <!-- 表单域 里面  prop要写要检验的字段名  放置 input/select/checkbox 相当于一行-->
        <el-form-item prop="mobile">
           <el-input v-model="loginForm.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>
        <!-- 表单域 -->
        <el-form-item prop="code">
          <el-input v-model="loginForm.code" style="width:65%" placeholder="验证码"></el-input>
            <el-button style="float:right" plain>发送验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <!-- 复选框 -->
          <el-checkbox v-model="loginForm.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button @click="submitLogin" type="primary" style="width:100%">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        mobile: '', // 手机号
        code: '', // 验证码
        check: false // 是否勾选 同意被坑
      },
      loginRules: {
        // 验证规则对象 key(字段名):value(规则 => [])
        mobile: [{ required: true, message: '请输入您的手机号', trigger: 'blur' }, {
          pattern: /^1[3456789]\d{9}$/, message: '手机号格式不正确', trigger: 'blur'
        }],
        code: [{ required: true, message: '请输入你的验证码', trigger: 'blur' }, {
          pattern: /^\d{6}$/, message: '验证码格式不正确', trigger: 'blur'
        }],
        check: [{ validator: function (rule, value, callback) {
          // 自定义校验函数
          // rule 规则 没啥用
          // value 要校验的字段的  值
          // callback 是一个回调函数
          if (value) {
            // 认为已经勾选
            callback() // 认为当前的规则校验通过了
          } else {
            // 认为没有勾选
            callback(new Error('您应该同意我们的霸王条款,让我们欺负你')) // 如果没有勾选 认为当前校验失败 应该停止
          }
        } }]

      }
    }
  },
  methods: {
    submitLogin () {
    //  手动校验
      this.$refs.myForm.validate((isOK) => {
        if (isOK) {
          //  说明校验通过  应该调用登录接口
          // axios  body参数 get参数地址参数 路由参数  查询参数
          // body参数 axios  data
          // get参数  axios params
          this.$axios({
            url: '/authorizations', // 请求地址 axios 没有指定 类型 默认走get类型
            method: 'post', // 类型
            data: this.loginForm // body 参数
          }).then(result => {
            // 只接受正确结果
            // 前端缓存 登录成功返回给我们的令牌
            window.localStorage.setItem('user-token', result.data.token)
            this.$router.push('/home') // 跳转到home页
          })
        }
      })
    }
  }
}
</script>

<style lang='less' scoped>
  .login  {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    &:before {
     background-image: url('../../assets/img/back.jpg');
     background-size: cover;
     filter: blur(10px);
     content: '';
     width:100%;
     height: 100%;
     left:0;
     top:0;
     position: absolute;

    }
    .login-card {
      width: 440px;
      height: 350px;
      z-index: 2;
      background-color: transparent;
      .title {
        text-align: center;
        margin-bottom: 30px;
        img {
          height: 45px;
        }
      }
    }
  }
</style>

```

### material

```html
<template>
  <el-card v-loading="loading">
    <!-- 头部内容 -->
    <bread-crumb slot="header">
      <template slot="title">素材管理</template>
    </bread-crumb>
    <!-- 上传 -->
    <el-row type='flex' justify="end">
      <el-upload action="" :http-request="uploadImg" :show-file-list="false">
        <el-button size="small" type="primary">上传图片</el-button>
      </el-upload>
    </el-row>

    <!-- 标签页 -->
    <el-tabs v-model="activeName" @tab-click="changeTab">
      <!-- 标签 -->
      <el-tab-pane label="全部图片" name="all">
        <!-- 生成页面结构 -->
        <div class="img-list">
          <!-- v-for对数据进行遍历 -->
          <el-card class="img-card" v-for="(item,index) in list" :key="item.id">
            <img @click="openDialog(index)" :src="item.url" alt />
            <el-row class="operate" type="flex" align="middle" justify="space-around">
              <!-- 需要根据当前是否收藏的状态来决定 是否给字体颜色 -->
              <i @click="collectOrCancel(item)" :style="{ color: item.is_collected ? 'red' : '#000' }" class="el-icon-star-on"></i>
              <i @click="delMaterial(item.id)" class="el-icon-delete-solid"></i>
            </el-row>
          </el-card>
        </div>
      </el-tab-pane>
      <el-tab-pane label="收藏图片" name="collect">
        <div class="img-list">
          <!-- v-for对数据进行遍历 -->
          <el-card class="img-card" v-for="item in list" :key="item.id">
            <img @click="openDialog(index)" :src="item.url" alt />
          </el-card>
        </div>
      </el-tab-pane>
    </el-tabs>
    <!-- 公共分页组件 -->
    <el-row type="flex" justify="center">
      <el-pagination
        :current-page="page.currentPage"
        :page-size="page.pageSize"
        :total="page.total"
        @current-change="changePage"
        background
        layout="prev, pager, next"
      ></el-pagination>
    </el-row>
    <el-dialog @opened="openEnd" :visible="dialogVisible" @close="dialogVisible = false">
       <el-carousel ref="myCarosel" indicator-position="outside" height="500px">
         <el-carousel-item v-for="(item,index) in list" :key="index">
           <img style="width:100%;height:100%" :src="item.url" alt="">
       </el-carousel-item>
      </el-carousel>
    </el-dialog>
  </el-card>
</template>

<script>
export default {
  data () {
    return {
      dialogVisible: false, // 弹层显示隐藏
      loading: false,
      activeName: 'all', // 当前选中的标签
      list: [], // 接收素材数据
      page: {
        currentPage: 1,
        pageSize: 8,
        total: 0
      },
      clickIndex: -1 // 点击的index
    }
  },
  methods: {
    openEnd () {
      // 此时已经可以获取走马灯实例了 ref
      this.$refs.myCarosel.setActiveItem(this.clickIndex)
    },
    // 打开弹层
    openDialog (index) {
      this.dialogVisible = true // dialog是懒加载 => 第一次没有弹出之前 是没有组件元素的
      // 没有办法在弹层中立刻做设置索引
      this.clickIndex = index // 存储一下 点击索引
    },
    // 删除用户图片素材
    async delMaterial (id) {
      await this.$confirm('你确定要删除此图片吗?')
      await this.$axios({
        method: 'delete',
        url: `/user/images/${id}`
      })
      this.getMaterial() // 重新拉取数据
    },
    // 取消或者收藏
    async collectOrCancel (item) {
      // item.iscollected true => 取消收藏 ? 收藏
      await this.$axios({
        method: 'put',
        url: `/user/images/${item.id}`,
        data: {
          collect: !item.is_collected // 取反 因为 收藏  =>取消收藏
        }
      })
      this.getMaterial() // 重新拉取数据
    },
    // 上传图片方法
    async uploadImg (params) {
      this.loading = true // 先弹个层
      let data = new FormData()
      data.append('image', params.file) // 文件加入到参数中
      await this.$axios({
        method: 'post',
        url: '/user/images',
        data
      })
      this.loading = false // 关闭弹层
      this.getMaterial() // 直接调用拉取数据的方法
    },
    // 改变页码方法
    changePage (newPage) {
      this.page.currentPage = newPage
      this.getMaterial()
    },
    // 切换页签方法
    changeTab () {
      this.page.currentPage = 1 // 重置回第一页
      this.getMaterial() // 调用获取数据方法
    },
    // 获取素材的方法
    async getMaterial () {
      let result = await this.$axios({
        url: '/user/images',
        params: {
          page: this.page.currentPage,
          per_page: this.page.pageSize,
          collect: this.activeName === 'collect' // 传false是获取所有的数据 传true是获取收藏数据
        }
      })
      this.list = result.data.results // 获取图片数据 有可能是 全部 也由可能是收藏
      this.page.total = result.data.total_count // 总条数
    }
  },
  created () {
    this.getMaterial()
  }
}
</script>

<style lang='less' scoped>
.img-list {
  display: flex;
  flex-wrap: wrap;
  .img-card {
    width: 200px;
    height: 220px;
    margin: 20px 50px;
    position: relative;
    img {
      width: 100%;
      height: 100%;
    }
    .operate {
      width: 100%;
      position: absolute;
      left: 0;
      bottom: 0;
      font-size: 20px;
      height: 36px;
      background-color: #f4f5f6;
      i {
        cursor: pointer;
      }
    }
  }
}
</style>

```

### picture

```html
<template>
  <el-card>
      <bread-crumb slot='header'>
        <template slot='title'>图文数据</template>
      </bread-crumb>
       <div   ref="myChart" class='echarts'></div>
       <div ref="myChart2" class='echarts'></div>

  </el-card>
</template>

<script>
import echarts from 'echarts'
export default {
  data () {
    return {
      optionData: {
        tooltip: {
          trigger: 'item',
          formatter: '{a} <br/>{b}: {c} ({d}%)'
        },
        legend: {
          orient: 'vertical',
          x: 'left',
          data: ['直接访问', '邮件营销', '联盟广告', '视频广告', '搜索引擎']
        },
        series: [
          {
            name: '访问来源',
            type: 'pie',
            radius: ['50%', '70%'],
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: false,
                position: 'center'
              },
              emphasis: {
                show: true,
                textStyle: {
                  fontSize: '30',
                  fontWeight: 'bold'
                }
              }
            },
            labelLine: {
              normal: {
                show: false
              }
            },
            data: [
              { value: 335, name: '直接访问' },
              { value: 310, name: '邮件营销' },
              { value: 234, name: '联盟广告' },
              { value: 135, name: '视频广告' },
              { value: 1548, name: '搜索引擎' }
            ]
          }
        ]
      }
    }
  },
  mounted   () {
    this.myChart = echarts.init(this.$refs.myChart) // 完成图表的初始化
    this.myChart2 = echarts.init(this.$refs.myChart2) // 完成图表的初始化

    this.myChart.setOption({
      title: {
        text: '测试数据',
        textStyle: {
          color: 'red'
        }
      },

      xAxis: {
        type: 'category',
        boundaryGap: false,
        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
      },
      yAxis: {
        type: 'value'
      },
      series: [{
        data: [820, 932, 901, 934, 1290, 1330, 1320],
        type: 'line',
        areaStyle: {}
      }]
    })

    this.myChart2.setOption(this.optionData) // 第一次设置
    setInterval(() => {
      this.optionData.series.data = [
        { value: 335, name: '直接访问' },
        { value: 310, name: '邮件营销' },
        { value: 234, name: '联盟广告' },
        { value: 135, name: '视频广告' },
        { value: 1548, name: '搜索引擎' }
      ].map(item => {
        item.value = item.value * parseInt(Math.random() * 5 * 100 / 50)
        return item
      })

      // this.optionData
      this.myChart2.setOption(this.optionData) // 每秒去设置
    }, 1000)
  }
}
</script>

<style>
 .echarts {
     width:800px;
     height: 400px;
 }
</style>

```

### publish

```html
<template>
  <el-card v-loading="loading">
      <bread-crumb slot='header'>
        <template slot='title'>
            发布文章
        </template>
      </bread-crumb>
      <!-- 容器 -->
      <el-form ref="publishForm" :model="formData" :rules="publishRules" style="margin-left:50px" label-width="100px">
          <el-form-item prop="title" label="标题">
              <el-input v-model="formData.title" style="width:60%"></el-input>
          </el-form-item>
          <el-form-item prop="content" label="内容">
                <quill-editor
                v-model="formData.content"
                style="height:300px"
                ></quill-editor>
          </el-form-item>
          <el-form-item style="margin-top:120px"  prop="cover" label="封面">
              <el-radio-group @change="changeType"  v-model="formData.cover.type">
                  <!-- // 封面类型 -1:自动，0-无图，1-1张，3-3张 -->
                  <el-radio :label="1">单图</el-radio>
                  <el-radio :label="3">三图</el-radio>
                  <el-radio :label="0">无图</el-radio>
                  <el-radio :label="-1">自动</el-radio>
              </el-radio-group>
          </el-form-item>
          <!-- 封面组件 -->
          <cover-image @selectTwoImg="receiveImg" :list="formData.cover.images"></cover-image>
          <el-form-item prop="channel_id" label="频道">
              <el-select v-model="formData.channel_id">
                  <el-option v-for="item in channels" :value="item.id" :label="item.name" :key="item.id"></el-option>
              </el-select>
          </el-form-item>
          <el-form-item>
              <el-button @click="publishArticle()" type='primary'>发布</el-button>
              <el-button @click="publishArticle(true)">存入草稿</el-button>

          </el-form-item>
      </el-form>
  </el-card>
</template>

<script>
import { getChannels } from '../../actions/articles'
export default {
  data () {
    return {
      loading: false,
      channels: [], // 接收频道数据
      formData: {
        title: '', // 文章标题
        content: '', // 文章内容
        cover: {
          type: 0, // 封面类型 -1:自动，0-无图，1-1张，3-3张
          images: [] // 放置封面地址的数组
        },
        channel_id: null // 频道id
      },
      publishRules: {
        //   校验规则 title/content/channel_id 必填项
        title: [{ required: true, message: '文章标题不能为空' }, {
          min: 5,
          max: 30,
          message: '标题的长度在5到30个字符之间'
        }],
        content: [{ required: true, message: '文章内容不能为空' }],
        channel_id: [{ required: true, message: '文章频道不能为空' }]
      }
    }
  },
  // beforeRouteUpdate (to, from, next) {
  //   console.log(to)
  //   next()
  // },
  watch: {
    // 处理 两个地址对应同一个组件跳转的时候 组件不销毁 但是数据没有重置的问题
    $route: function (to, from) {
      if (to.params.articleId) {
        // 是修改
      } else {
        // 是发布
        this.formData = {
          title: '', // 文章标题
          content: '', // 文章内容
          cover: {
            type: 0, // 封面类型 -1:自动，0-无图，1-1张，3-3张
            images: [] // 放置封面地址的数组
          },
          channel_id: null // 频道id
        }
      }
    }
    // // 监听 封面类型的改变
    // 'formData.cover.type': function () {
    //   if (this.formData.cover.type === 0 || this.formData.cover.type === -1) {
    //     this.formData.cover.images = [] // 无图或者自动
    //   } else if (this.formData.cover.type === 1) {
    //     this.formData.cover.images = [''] // 单图
    //   } else if (this.formData.cover.type === 3) {
    //     this.formData.cover.images = ['', '', ''] // 3图
    //   }
    // }
  },
  methods: {
    // 接收子组件数据
    receiveImg (url, index) {
      // 现在拿到的url地址 还要拿到下标
      // 但是要改的是数组
      // this.formData.cover.images[index] = url //  这种写法 错误!!!!! 不能保证每次都成功
      // 响应式数据 => 数据变化 => 视图变化
      // 数据变化 =>vuejs => 检测到了数据变化 =>vuejs 对于数组的检测变化 不能通过索引来处理
      // Vuejs会检测到 新数组 替换原数组 => 进行响应式更新
      // this.formData.cover.images = this.formData.cover.images.map(function (item, i) {
      //   if (index === i) {
      //     // 说明找到了要替换的地址
      //     return url
      //   }
      //   // 如果没找到 要直接返回原来的数据
      //   return item
      // })
      this.formData.cover.images = this.formData.cover.images.map((item, i) => i === index ? url : item)
    },
    changeType () {
      if (this.formData.cover.type === 0 || this.formData.cover.type === -1) {
        this.formData.cover.images = [] // 无图或者自动
      } else if (this.formData.cover.type === 1) {
        this.formData.cover.images = [''] // 单图
      } else if (this.formData.cover.type === 3) {
        this.formData.cover.images = ['', '', ''] // 3图
      }
    },
    //   获取所有的频道
    async getChannels () {
      let result = await getChannels()
      this.channels = result.data.channels
    },
    // 发布文章 发布到草稿 /正式文章
    publishArticle (draft) {
      this.$refs.publishForm.validate(isOK => {
        if (isOK) {
          // 判断是修改还是发布文章
          let { articleId } = this.$route.params // 获取动态路由参数
          this.$axios({
            url: articleId ? `/articles/${articleId}` : '/articles',
            method: articleId ? 'put' : 'post',
            params: { draft }, // 查询参数
            data: this.formData // 请求体参数
          }).then(result => {
            this.$message({
              type: 'success',
              message: '保存成功'
            })
            // 跳转到文章列表页
            this.$router.push('/home/articles')
          })
          // if (articleId) {
          //   // 修改文章接口
          //   this.$axios({
          //     url: `/articles/${articleId}`,
          //     params: { draft }, // 查询参数
          //     data: this.formData // 请求体参数
          //   }).then(result => {
          //     this.$message({
          //       type: 'success',
          //       message: '保存成功'
          //     })
          //     // 跳转到文章列表页
          //     this.$router.push('/home/articles')
          //   })
          // } else {
          //   // 调用发布接口
          //   this.$axios({
          //     url: '/articles',
          //     method: 'post',
          //     params: { draft }, // 查询参数
          //     data: this.formData // 请求体参数
          //   }).then(() => {
          //     this.$message({
          //       type: 'success',
          //       message: '保存成功'
          //     })
          //     // 跳转到文章列表页
          //     this.$router.push('/home/articles')
          //   })
          // }
        }
      })
    },
    // 通过id查询文章数据
    getArticleById (articleId) {
      this.loading = true
      this.$axios({
        url: `/articles/${articleId}`
      }).then(result => {
        this.loading = false
        this.formData = result.data // 将数据赋值data
      })
    }
  },
  created () {
    this.getChannels()
    let { articleId } = this.$route.params // 获取动态路由参数
    articleId && this.getArticleById(articleId) // 如果文章id存在 直接查询文章的数据
  }
}
</script>

<style>

</style>

```

### 404.vue

```html
<template>
  <div class='back'></div>
</template>

<script>
export default {

}
</script>

<style scoped>
.back {
    height: 100vh;
    background-image: url('../assets/img/404.png');
    background-size: cover;
}
</style>

```

## utils

### eventBus

```js
// 公共实例
import Vue from 'vue'
export default new Vue() // 公共实例 => 实例化了一个Vue
```



### request

```js
// 封装一个axios
import axios from 'axios'
import router from '../router'
import { Message } from 'element-ui'
import JSONBig from 'json-bigint' // 引入第三方的包
axios.defaults.baseURL = 'http://ttapi.research.itcast.cn/mp/v1_0' // 设置一个常态值

// 请求拦截器
axios.interceptors.request.use(function (config) {
  // 执行请求ok
  // config 请求参数配置
  let token = window.localStorage.getItem('user-token')// 取token
  config.headers.Authorization = `Bearer ${token}` // 统一注入token
  return config // 表示会用该config请求进行后台操作
}, function () {
  // 执行请求错误

})

axios.defaults.transformResponse = [function (data) {
  return data ? JSONBig.parse(data) : {} // 解决js处理大数字失真问题
}]

// 响应拦截器
axios.interceptors.response.use(function (response) {
  // 成功时执行该函数 状态码 200 /201 /204

  return response.data ? response.data : {}
}, function (error) {
  // 失败时执行该函数
  let status = error.response.status
  let message = ''
  switch (status) {
    case 400:
      message = '请求参数错误'
      break
    case 507:
      message = '服务器数据库异常'
      break
    case 401:
      // token过期或者失效
      // this.$router
      window.localStorage.removeItem('user-token') // 删除过期的token
      router.push('/login') // 跳转到登录页
      break
    case 403:
      message = '没有设置这条评论的权限'
      break
    default:
      break
  }
  Message({ type: 'warning', message }) // 提示信息
  // 这里需要注意 错误执行函数 如果不做任何操作 还会进入到promise then中
  return Promise.reject(error) // 只要reject =>catch
})
export default axios

```

## styles(less)

```less
body {
    margin: 0;
    padding: 0;
  }
  *,
  *:before,
  *:after {
    box-sizing: inherit;
  }
  
  li {
    list-style: none;
  }
  dl,
  dd,
  dt,
  ul,
  li {
    margin: 0;
    padding: 0;
  }
  
  .no-padding {
    padding: 0px !important;
  }
  
  .padding-content {
    padding: 4px 0;
  }
  
  a:focus,
  a:active {
    outline: none;
  }
  
  a,
  a:focus,
  a:hover {
    cursor: pointer;
    color: inherit;
    text-decoration: none;
  }
  
  b {
    font-weight: normal;
  }
  
  div:focus {
    outline: none;
  }
  
  .fr {
    float: right;
  }
  
  .fl {
    float: left;
  }
  
  .pr-5 {
    padding-right: 5px;
  }
  
  .pl-5 {
    padding-left: 5px;
  }
  
  .block {
    display: block;
  }
  
  .pointer {
    cursor: pointer;
  }
  
  .inlineBlock {
    display: block;
  }
  
```

## router

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import Home from '../views/home'
import Login from '../views/login'
import Home2 from '../views/home/home.vue'
Vue.use(VueRouter)

const routes = [
  {
    path: '/',
    redirect: '/home' // 强制跳转
  },
  {
    path: '*',
    component: () => import('../views/404')
  },
  {
    path: '/home',
    name: 'home',
    component: Home,
    children: [{
      path: '', // 二级路由地址什么都不写  代表二级路由默认的组件
      component: Home2
    }, {
      path: 'comment', // 完整 相对
      component: () => import('../views/comment')
    }, {
      path: 'material',
      component: () => import('../views/material')
    }, {
      path: 'articles', // 文章列表
      component: () => import('../views/articles')
    }, {
      path: 'publish', // 发布文章
      component: () => import('../views/publish')
    }, {
      path: 'publish/:articleId', // 修改文章
      component: () => import('../views/publish')
    }, {
      path: 'account',
      component: () => import('../views/account')
    }, {
      path: 'picture',
      component: () => import('../views/picture')
    }]
  }, {
    path: '/login',
    component: Login
  }
  // {
  //   path: '/about',
  //   name: 'about',
  //   // route level code-splitting
  //   // this generates a separate chunk (about.[hash].js) for this route
  //   // which is lazy-loaded when the route is visited.
  //   component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  // }
]

const router = new VueRouter({
  routes
})

export default router

```

## permission

```js

// 处理路由拦截器 导航守卫
import router from '../router'
import progresss from 'nprogress'
import 'nprogress/nprogress.css'
// 全局前置守卫  当 路由发生变化时 这个方法里的回调函数就会执行
router.beforeEach(function (to, from, next) {
  progresss.start() // 开启进度条
  // 权限拦截 认为有token 让过去 没token不让过
  if (to.path.startsWith('/home')) {
    //   确定要去检查的范围
    let token = window.localStorage.getItem('user-token')
    if (token) {
      next() // 放过
    } else {
      next('/login') // 跳转到登录页
    }
  } else {
    next() // 直接放过
  }
})
router.afterEach(() => {
  // setTimeout(() => progresss.done(), 1000)
  progresss.done()
  // 关闭进度条
})

```

## constant(API.js)

```js

export const API_ARTICLES = '/articles' // 设置一个常量  作为请求地址
export const API_CHANNELS = '/channels' // 频道地址
```

## components

### common(bread-crumb)

```html
<template>
  <!-- 封装原来的el-breadcrumb -->
<el-breadcrumb separator=">">
    <el-breadcrumb-item to="/home">首页</el-breadcrumb-item>
    <el-breadcrumb-item>
        <!-- 定义一个具名插槽 -->
        <slot name='title'></slot>
    </el-breadcrumb-item>
 </el-breadcrumb>
</template>

<script>
export default {

}
</script>

<style>

</style>

```

### home

#### layout-aside.vue

```html
<template>
  <div class='layout-aside'>
      <div class='title'>
          <img :src="collapse ? smallImg : bigImg" alt="">
      </div>
      <!-- 左侧导航组件  开启路由 :router="true" 或者 router-->
      <el-menu :collapse="collapse" router background-color="#353b4e" text-color="#adafb5" active-text-color="#ffd04b">
          <!-- 没有折叠选项 -->
          <el-menu-item index="/home">
          <i class='el-icon-s-home'></i>
          <span>首页</span></el-menu-item>
          <!-- 二级折叠菜单 -->
          <el-submenu index="1">
              <!-- 具名插槽 -->
              <template  slot='title'>
                    <i   class='el-icon-document-copy'></i>
                 <span>内容管理</span>
              </template>
              <!-- 匿名插槽 -->
             <el-menu-item index="/home/publish">发布文章</el-menu-item>
             <el-menu-item index="/home/articles">文章列表</el-menu-item>
             <el-menu-item index="/home/comment">评论管理</el-menu-item>
             <el-menu-item index="/home/material">素材管理</el-menu-item>

          </el-submenu>
          <el-submenu index="2">
              <!-- 具名插槽 -->
              <template slot='title'>
                <i class='el-icon-female'></i>
                 <span >粉丝管理</span>
              </template>
              <!-- 匿名插槽 -->
             <el-menu-item index="/home/picture">图文数据</el-menu-item>
             <el-menu-item index="/home/fansinfo">粉丝概况</el-menu-item>
             <el-menu-item index="/home/fanspicture">粉丝画像</el-menu-item>
             <el-menu-item index="/home/fanslist">粉丝列表</el-menu-item>
          </el-submenu>
          <el-menu-item index="/home/account">
          <i class='el-icon-s-custom'></i>
          <span>账户信息</span>
          </el-menu-item>

      </el-menu>
  </div>
</template>

<script>
export default {
  props: ['collapse'],
  data () {
    return {
      bigImg: require('../../assets/img/logo_admin.png'),
      smallImg: require('../../assets/img/toutiao.png')
    }
  }
}
</script>

<style lang='less' scoped>
 .layout-aside {
    //  width: 230px;
     .el-menu {
       border-right:none;
     };
     .title {
         background-color: #2e2f32;
         text-align: center;
         padding: 10px 0;
         img {
             height: 35px;
         }
     }
 }
</style>

```



#### layout-header.vue

```html
<template>
<!-- el-row -->
  <el-row class='layout-header' type='flex' align="middle">
      <!-- 先定义一行 -->
     <el-col class='left' :span="12">
         <i @click="collapseOrOpen" :class="{'el-icon-s-unfold': collapse,'el-icon-s-fold': !collapse}"></i>
         <span>江苏传智播客教育科技股份有限公司</span>
     </el-col>
     <el-col class='right' :span="12">
         <el-row type='flex' justify="end" align="middle">
             <img :src="userInfo.photo ? userInfo.photo : defaultImg" alt="">
             <!-- 下拉菜单 -->
             <el-dropdown @command="clickMenu">
                 <!-- 匿名插槽  下拉菜单显示的元素内容 -->
                 <span>{{ userInfo.name }}</span>
                 <el-dropdown-menu slot="dropdown">
                     <el-dropdown-item command="info">个人信息</el-dropdown-item>
                     <el-dropdown-item command="git">git地址</el-dropdown-item>
                     <el-dropdown-item command="lgout">退出</el-dropdown-item>
                 </el-dropdown-menu>
             </el-dropdown>
         </el-row>
     </el-col>

  </el-row>
</template>

<script>
import eventBus from '../../utils/eventBus'
export default {
  data () {
    return {
      collapse: false, // 默认是展开
      userInfo: {}, // 定义一个用户对象
      defaultImg: require('../../assets/img/header.jpg') // 先将图片转化成了一个变量
    }
  },
  created () {
    this.getUserInfo()
    // 开启监听
    eventBus.$on('updateUserInfo', () => {
      // 认为别人更新了数据 自己也应该更新
      this.getUserInfo()
    })
  },
  methods: {
    // 折叠或者 展开
    collapseOrOpen () {
      this.collapse = !this.collapse // 不是展开就是折叠
      eventBus.$emit('changeCollapse') // 触发一个事件
    },
    getUserInfo () {
      this.$axios({
        url: '/user/profile'
      }).then(result => {
        this.userInfo = result.data
      })
    },
    //   点击菜单项时触发
    clickMenu (command) {
      if (command === 'info') {
        this.$router.push('/home/account') // 去到账户信息
      } else if (command === 'git') {
        //   跳转到git地址
        window.location.href = 'https://github.com/shuiruohanyu/90heimatoutiao'
      } else {
        //    退出
        window.localStorage.removeItem('user-token') // 删除令牌
        this.$router.push('/login') // 回到登录页
      }
    }
  }
}
</script>

<style lang='less' scoped>
.layout-header {
    height:60px;
    .left {
        font-size: 20px;
        span {
           color: #2c3e50;
           font-size: 16px;
           margin-left:4px;
        }
    }
    .right {
      img {
          width: 40px;
          height: 40px;
          border-radius: 50%;
          margin-right: 5px;
      }
    }
}
</style>

```

### publish

#### cover-image.vue

```html
<template>
  <div class='cover-image'>
    <div @click="openDialog(index)" v-for="(item,index) in list" :key="index" class='cover-image-item'>
      <img :src="item ? item : defaultImg" alt="">
    </div>
    <!-- 放置一个对话框 -->
    <el-dialog :visible="dialogVisible" @close="closeDialog" >
          <!-- 放置另外一个组件 素材库组件 和上传组件 -->
          <!-- 监听谁的事件就在谁的标签上写监听 -->
           <select-image @selectOneImg="receiveImg"></select-image>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: ['list'],
  data () {
    return {
      defaultImg: require('../../assets/img/pic_bg.png'),
      dialogVisible: false, // 用来控制弹层的开关
      selectIndex: -1 // 用来存储点击的哪个图片的下标
    }
  },
  methods: {
    // 接收方法
    receiveImg (url) {
      // props  只能读取 不能修改
      this.$emit('selectTwoImg', url, this.selectIndex) // 再次传递
      this.closeDialog() // 关闭弹层
    },
    openDialog (index) {
      this.dialogVisible = true // 打开弹层
      this.selectIndex = index // 记录当前点击的是哪个图片
    },
    closeDialog () {
      this.dialogVisible = false // 关闭弹层
    }
  }
}
</script>

<style lang='less' scoped>
   .cover-image {
     margin: 20px 100px;
     display: flex;
     .cover-image-item {
       border: 1px solid #ccc;
       width: 250px;
       height: 250px;
       padding: 20px;
       img {
         width: 100%;
         height: 100%;
       }
     }
   }
</style>

```

#### select-image.vue

```html
<template>
  <el-tabs v-model="activeName">
    <el-tab-pane label="素材库" name="material">
      <!-- 外层容器 -->
      <div class="select-image-list">
        <!-- 循环生成多个el-card -->
        <el-card v-for="item in list" :key="item.id" class="img-card">
            <!-- 给图片注册点击事件 -->
          <img @click="clickImg(item.url)" :src="item.url" alt />
        </el-card>
      </div>
      <!-- 放置一个分页组件 -->
      <el-row type="flex" justify="center">
        <el-pagination background layout="prev, pager, next"
         :total="page.total"
         :current-page="page.currentPage"
         :page-size="page.pageSize"
         @current-change="changePage"
         ></el-pagination>
      </el-row>
    </el-tab-pane>
    <el-tab-pane label="上传图片" name="upload">
      <!-- 给action不报错 -->
      <el-upload action="" :http-request="uploadImg" class='upload-img' :show-file-list="false">
        <i class='el-icon-plus'></i>
      </el-upload>
    </el-tab-pane>
  </el-tabs>
</template>

<script>
export default {
  data () {
    return {
      activeName: 'material', // 默认选中是素材库
      list: [], // 接收素材管理的数据
      page: {
        currentPage: 1, // 默认请求页码
        pageSize: 8,
        total: 0 // 总页码
      }
    }
  },
  methods: {
    // 上传组件方法
    uploadImg (params) {
      let data = new FormData()
      data.append('image', params.file) // 加入参数
      this.$axios({
        url: '/user/images',
        method: 'post',
        data
      }).then(result => {
        // result.data.url
        this.$emit('selectOneImg', result.data.url) // 自定义事件名 可以不用全小写了
      })
    },
    //   点击图片时触发
    clickImg (url) {
      //  点击图片时  => 要把图片传给显示的封面 自定义事件
      this.$emit('selectOneImg', url) // 自定义事件名 可以不用全小写了
    },
    //   改变页码事件
    changePage (newPage) {
      this.page.currentPage = newPage
      this.getAllImg()
    },
    //   获取所有素材
    getAllImg () {
      this.$axios({
        url: '/user/images',
        params: { collect: false, page: this.page.currentPage, per_page: this.page.pageSize }
      }).then(result => {
        this.list = result.data.results
        this.page.total = result.data.total_count // 获取总数
      })
    }
  },
  created () {
    this.getAllImg()
  }
}
</script>

<style lang='less' scoped>
.select-image-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  .img-card {
    width: 150px;
    height: 150px;
    margin: 20px 0;
    img {
      width: 100%;
      height: 100%;
    }
  }
}
.upload-img {
  display: flex;
  justify-content: center;
  i {
    font-size:50px;
    padding: 50px;
    border:1px dashed #ccc;
    border-radius: 4px;
  }
}
</style>

```



### inex.js(components文件夹下的)

```js
import layoutAside from './home/layout-aside'
import layoutHeader from './home/layout-header'
import breadCrumb from './common/bread-crumb'
import { quillEditor } from 'vue-quill-editor' // quill编辑器组件对象
import CoverImage from './publish/cover-image'
import SelectImage from './publish/select-image'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'
export default {
  install (Vue) {
    Vue.component('layout-aside', layoutAside) // 注册一个全局组件
    Vue.component('layout-header', layoutHeader) // 注册一个全局组件
    Vue.component('bread-crumb', breadCrumb) // 全局注册一个面包屑组件
    Vue.component('quill-editor', quillEditor) // 注册一个全局的富文本编辑器
    Vue.component('cover-image', CoverImage) // 注册一个封面组件
    Vue.component('select-image', SelectImage) // 注册一个素材库和上传图片组件
  }
}

```

## actions(articles.js)

```js
// 专门放置文章请求的
// 获取文章
import request from '../utils/request'
import { API_ARTICLES, API_CHANNELS } from '../constant/API'
export function getArticles (params) {
  return request({
    url: API_ARTICLES,
    params
  })
}
// 获取频道数据
export function getChannels () {
  return request({
    url: API_CHANNELS
  })
}

```

## assets=>img=>放置各种图片