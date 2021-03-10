# Headline

> An awesome project.
---
# 主题列表：juejin, github, smartblue, cyanosis, channing-cyan, fancy, hydrogen, condensed-night-purple, greenwillow
# 贡献主题：https://github.com/xitu/juejin-markdown-themes
theme: juejin
highlight:
---

### 各种干货视频及各种软件安装包地址

* [后台系统的权限控制与管理【完结】](https://www.bilibili.com/video/BV15Q4y1K79c?from=search&seid=13581687011867552931)
* [vue3正式版教程【李南江版】](https://www.bilibili.com/video/BV14k4y117LL?from=search&seid=770007897900796550)
* [git各版本下载地址【全版本】](https://npm.taobao.org/mirrors/git-for-windows/)

#### document.body.style.overflow = "hidden"; //禁止主页面滚动

### 解决因为本地代码和远程代码冲突，导致git pull无法拉取远程代码的问题
[原文出处地址](https://www.cnblogs.com/zhujiabin/p/9140863.html)
1. git stash 将本地代码stash到仓库中。可以使用git stash save ***定义自己的标记，方便以后查询
2. git pull 将远程代码拉取到本地。
3. git stash pop 将仓库中的代码合到本地最新代码中。
4. 在处理bug的过程中，可能存在多次stash的操作。这时可以使用git stash list查看本地仓库中都存储了几个stash版本。
5. git stash pop默认将最近一次stash操作合并到本地代码中，也可以通过git stash pop stash@{Number}指定将某次    stash的内容合并到本地代码中。
6. git stash pop命令在合并代码的同时，会把仓库中对应的内容弹出。如果只想查看，而不想弹出内容，可以使用git stash apply命令进行操作。
7. git stash -h 查看git stash帮助
8. git stash show 显示stash合并到本地代码后，哪些文件会修改，以及修改的概述
9. git stash show -p stash@{0} 显示修改的详细内
### a标签下载文件
```
handleOk() {
      let link = document.createElement("a");
      link.download = "附件1.xls";  //下载文件名
      link.href = "附件1.xls";  // 提供文件地址，或者后端接口地址
      document.body.appendChild(link);
      link.click();
},
```
### 前端实现分页（结合element-ui分页器实现）
```
data(){
  currentPageData:[],//当前页数据
  allData:[],//全部数据
  currentPage: 1, //当前页
  pageSize: 10, //每页显示数据
  total: 20, //总数
}
mounted() {
  this.setCurrentPageData();
},
methods:{
  // 切换每页展示多少条数据
  handleSizeChange(val) {
    this.pageSize = val;
    this.setCurrentPageData();
    console.log(`每页 ${val} 条`);
  },
  // 当前所在页
  handleCurrentChange(val) {
    this.currentPage = val;
    this.setCurrentPageData();
    console.log(`当前页: ${val}`);
  },
  // 设置当前页面数据，对数组操作的截取规则为[0~10],[10~20]...,
  setCurrentPageData() {
    let begin =(this.currentPage - 1) * this.pageSize;
    let end = this.currentPage * this.pageSize;
    this.currentPageData = this.allData.slice(begin, end);
  },
}
```
### 正则效验工具函数 
####  [参考地址](https://juejin.cn/post/6864357223733461005#heading-36)
#### 18位身份证效验
```
// 效验身份证号码
 cardid (code) {
  let data ={
    result:false,
    msg:""
  } 
  // let data.result = true
  // let data.msg = ''
  var city = {
    11: '北京',
    12: '天津',
    13: '河北',
    14: '山西',
    15: '内蒙古',
    21: '辽宁',
    22: '吉林',
    23: '黑龙江 ',
    31: '上海',
    32: '江苏',
    33: '浙江',
    34: '安徽',
    35: '福建',
    36: '江西',
    37: '山东',
    41: '河南',
    42: '湖北 ',
    43: '湖南',
    44: '广东',
    45: '广西',
    46: '海南',
    50: '重庆',
    51: '四川',
    52: '贵州',
    53: '云南',
    54: '西藏 ',
    61: '陕西',
    62: '甘肃',
    63: '青海',
    64: '宁夏',
    65: '新疆',
    71: '台湾',
    81: '香港',
    82: '澳门',
    91: '国外 '
  }

    if (code.length == 18) {
      if (!code || !/(^\d{18}$)|(^\d{17}(\d|X|x)$)/.test(code)) {
        data.msg = '证件号码格式错误'
      } else if (!city[code.substr(0, 2)]) {
        data.msg = '地址编码错误'
      } else {
        // 18位身份证需要验证最后一位校验位
        code = code.split('')
        // ∑(ai×Wi)(mod 11)
        // 加权因子
        var factor = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2]
        // 校验位
        var parity = [1, 0, 'X', 9, 8, 7, 6, 5, 4, 3, 2, 'x']
        var sum = 0
        var ai = 0
        var wi = 0
        for (var i = 0; i < 17; i++) {
          ai = code[i]
          wi = factor[i]
          sum += ai * wi
        }
        if (parity[sum % 11] != code[17]) {
          data.msg = '证件号码校验位错误'
        } else {
          data.result = true
        }
      }
    } else {
      data.msg = '证件号码长度不为18位'
    }

  return data
}
```
### 全局配置自定义指令
#### 1.设置工具函数
* utils/directives.js
```
import Vue from 'vue'

const trigger = (el, type) => {
  const e = document.createEvent('HTMLEvents')
  e.initEvent(type, true, true)
  el.dispatchEvent(e)
}

// input验证只能输入数字
Vue.directive('numberTwo', {
  bind(el) {
    const input = el.getElementsByTagName('input')[0]

    function del() {
      let value = input.value
      // 先把非数字的都替换掉，除了数字和.
      value = value.replace(/[^\d.]/g, '')
      // 保证只有出现一个.而没有多个.
      value = value.replace(/\.{2,}/g, '.')
      // 必须保证第一个为数字而不是.
      value = value.replace(/^\./g, '')
      // 保证.只出现一次，而不能出现两次以上
      value = value
        .replace('.', '$#$')
        .replace(/\./g, '')
        .replace('$#$', '.')
      // 只能输入两个小数
      value = value.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3')
      input.value = value
    }

    input.onkeyup = function(e) {
      del()
      trigger(input, 'input')
    }
    input.onblur = function(e) {
      del()
      trigger(input, 'input')
    }
  }
})
// 只能输入数字
Vue.directive('onlyNumber', {
  bind(el) {
    const input = el.getElementsByTagName('input')[0]

    function del() {
      let value = input.value
      value = value.replace(/\D/g, '')
      input.value = value
    }
    input.onkeyup = function(e) {
      del()
      trigger(input, 'input')
    }
    input.onblur = function(e) {
      del()
      trigger(input, 'input')
    }
  }
})
// 大于0小于1的一位小数
Vue.directive('numberOne', {
  bind(el) {
    const input = el.getElementsByTagName('input')[0]

    function del() {
      let value = input.value
      // 先把非数字的都替换掉，除了数字和.
      value = value.replace(/[^\d.]/g, '')
      // 保证只有出现一个.而没有多个.
      value = value.replace(/\.{2,}/g, '.')
      // 必须保证第一个为数字而不是.
      value = value.replace(/^\./g, '')
      // 保证.只出现一次，而不能出现两次以上
      value = value
        .replace('.', '$#$')
        .replace(/\./g, '')
        .replace('$#$', '.')
      // 只能输入两个小数
      value = value.replace(/^(\-)*(\d+)\.(\d).*$/, '$1$2.$3')
      if (value >= 1) value = 1
      input.value = value
    }

    input.onkeyup = function(e) {
      del()
      trigger(input, 'input')
    }
    input.onblur = function(e) {
      del()
      trigger(input, 'input')
    }
  }
})
// 验证输入数字且保留2位小数
Vue.directive('onlyTwoDecimal', {
  bind(el) {
    const input = el.getElementsByTagName('input')[0]
    function del() {
      let value = input.value
      // 先把非数字的都替换掉，除了数字和.
      value = value.replace(/[^\d.]/g, '')
      // 保证只有出现一个.而没有多个.
      value = value.replace(/\.{2,}/g, '.')
      // 必须保证第一个为数字而不是.
      value = value.replace(/^\./g, '')
      // 保证.只出现一次，而不能出现两次以上
      value = value
        .replace('.', '$#$')
        .replace(/\./g, '')
        .replace('$#$', '.')
      // 只能输入两个小数
      value = value.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3')
      input.value = value
    }
    input.onkeyup = function(e) {
      del()
      trigger(input, 'input')
    }
    input.onblur = function(e) {
      del()
      trigger(input, 'input')
    }
  }
})
```
#### 2.在main.js中全局引入
`import './utils/directives'`
#### 3.全局使用
**v-onlyNumber：**
`  <el-input v-model="formData.words" v-onlyNumber placeholder="请输入" />`
