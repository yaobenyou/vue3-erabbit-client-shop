# 结算&支付



## 01-结算-页面布局

![1615272228114](./docs/media/1615272228114.png)



落的代码：

1. 定义组件基础解构和配置路由

`src/views/member/pay/checkout.vue`  定义组件

```vue
<template>
  <div class="xtx-pay-checkout-page">
    <div class="container">
      <XtxBread>
        <XtxBreadItem to="/">首页</XtxBreadItem>
        <XtxBreadItem to="/cart">购物车</XtxBreadItem>
        <XtxBreadItem >填写订单</XtxBreadItem>
      </XtxBread>
      <div class="wrapper">
        <!-- 收货地址 -->
        <!-- 商品信息 -->
        <!-- 配送时间 -->
        <!-- 支付方式 -->
        <!-- 金额明细 -->
        <!-- 提交订单 -->
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'XtxPayCheckoutPage'
}
</script>
<style scoped lang="less">
.xtx-pay-checkout-page {
  .wrapper {
    background: #fff;
  }
}
</style>
```

`src/router/index.js`  配置路由

```js
const PayCheckout = () => import('@/views/member/pay/checkout')
```

```diff
      { path: '/cart', component: Cart },
+     { path: '/member/checkout', component: PayCheckout }
```

2. 完成页面布局效果

```vue
<template>
  <div class="xtx-pay-checkout-page">
    <div class="container">
      <XtxBread>
        <XtxBreadItem to="/">首页</XtxBreadItem>
        <XtxBreadItem to="/cart">购物车</XtxBreadItem>
        <XtxBreadItem >填写订单</XtxBreadItem>
      </XtxBread>
      <div class="wrapper">
        <!-- 收货地址 -->
        <h3 class="box-title">收货地址</h3>
        <div class="box-body">
          <div class="address">
            <div class="text">
              <!-- <div class="none">您需要先添加收货地址才可提交订单。</div> -->
              <ul>
                <li><span>收<i/>货<i/>人：</span>朱超</li>
                <li><span>联系方式：</span>132****2222</li>
                <li><span>收货地址：</span>海南省三亚市解放路108号物质大厦1003室</li>
              </ul>
              <a href="javascript:;">修改地址</a>
            </div>
            <div class="action">
              <XtxButton class="btn">切换地址</XtxButton>
              <XtxButton class="btn">添加地址</XtxButton>
            </div>
          </div>
        </div>
        <!-- 商品信息 -->
        <h3 class="box-title">商品信息</h3>
        <div class="box-body">
          <table class="goods">
            <thead>
              <tr>
                <th width="520">商品信息</th>
                <th width="170">单价</th>
                <th width="170">数量</th>
                <th width="170">小计</th>
                <th width="170">实付</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="i in 4" :key="i">
                <td>
                  <a href="javascript:;" class="info">
                    <img src="https://yanxuan-item.nosdn.127.net/cd9b2550cde8bdf98c9d083d807474ce.png" alt="">
                    <div class="right">
                      <p>轻巧多用锅雪平锅 麦饭石不粘小奶锅煮锅</p>
                      <p>颜色：白色 尺寸：10cm 产地：日本</p>
                    </div>
                  </a>
                </td>
                <td>&yen;100.00</td>
                <td>2</td>
                <td>&yen;200.00</td>
                <td>&yen;200.00</td>
              </tr>
            </tbody>
          </table>
        </div>
        <!-- 配送时间 -->
        <h3 class="box-title">配送时间</h3>
        <div class="box-body">
          <a class="my-btn active" href="javascript:;">不限送货时间：周一至周日</a>
          <a class="my-btn" href="javascript:;">工作日送货：周一至周五</a>
          <a class="my-btn" href="javascript:;">双休日、假日送货：周六至周日</a>
        </div>
        <!-- 支付方式 -->
         <h3 class="box-title">支付方式</h3>
        <div class="box-body">
          <a class="my-btn active" href="javascript:;">在线支付</a>
          <a class="my-btn" href="javascript:;">货到付款</a>
          <span style="color:#999">货到付款需付5元手续费</span>
        </div>
        <!-- 金额明细 -->
        <h3 class="box-title">金额明细</h3>
        <div class="box-body">
          <div class="total">
            <dl><dt>商品件数：</dt><dd>5件</dd></dl>
            <dl><dt>商品总价：</dt><dd>¥5697.00</dd></dl>
            <dl><dt>运<i></i>费：</dt><dd>¥0.00</dd></dl>
            <dl><dt>应付总额：</dt><dd class="price">¥5697.00</dd></dl>
          </div>
        </div>
        <!-- 提交订单 -->
        <div class="submit">
          <XtxButton type="primary">提交订单</XtxButton>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'XtxPayCheckoutPage'
}
</script>
<style scoped lang="less">
.xtx-pay-checkout-page {
  .wrapper {
    background: #fff;
    padding: 0 20px;
    .box-title {
      font-size: 16px;
      font-weight: normal;
      padding-left: 10px;
      line-height: 70px;
      border-bottom: 1px solid #f5f5f5;
    }
    .box-body {
      padding: 20px 0;
    }
  }
}
.address {
  border: 1px solid #f5f5f5;
  display: flex;
  align-items: center;
  .text {
    flex: 1;
    min-height: 90px;
    display: flex;
    align-items: center;
    .none {
      line-height: 90px;
      color: #999;
      text-align: center;
      width: 100%;  
    }
    > ul {
      flex: 1;
      padding: 20px;
      li {
        line-height: 30px;
        span {
          color: #999;
          margin-right: 5px;
          > i {
            width: 0.5em;
            display: inline-block;
          }
        }
      }
    }
    > a {
      color: @xtxColor;
      width: 160px;
      text-align: center;
      height: 90px;
      line-height: 90px;
      border-right: 1px solid #f5f5f5;
    }
  }
  .action {
    width: 420px;
    text-align: center;
    .btn {
      width: 140px;
      height: 46px;
      line-height: 44px;
      font-size: 14px;
      &:first-child {
        margin-right: 10px;
      }
    }
  }
}
.goods {
  width: 100%;
  border-collapse: collapse;
  border-spacing: 0;
  .info {
    display: flex;
    text-align: left;
    img {
      width: 70px;
      height: 70px;
      margin-right: 20px;
    }
    .right {
      line-height: 24px;
      p {
        &:last-child {
          color: #999;
        }
      }
    }
  }
  tr {
    th {
      background: #f5f5f5;
      font-weight: normal;
    }
    td,th {
      text-align: center;
      padding: 20px;
      border-bottom: 1px solid #f5f5f5;
      &:first-child {
        border-left: 1px solid #f5f5f5;
      }
      &:last-child {
        border-right: 1px solid #f5f5f5;
      }
    }
  }
}
.my-btn {
  width: 228px;
  height: 50px;
  border: 1px solid #e4e4e4;
  text-align: center;
  line-height: 48px;
  margin-right: 25px;
  color: #666666;
  display: inline-block;
  &.active,&:hover {
    border-color: @xtxColor;
  }
}
.total {
  dl {
    display: flex;
    justify-content: flex-end;
    line-height: 50px;
    dt {
      i {
        display: inline-block;
        width: 2em;
      }
    }
    dd {
      width: 240px;
      text-align: right;
      padding-right: 70px;
      &.price {
        font-size: 20px;
        color: @priceColor;
      }
    }
  }
}
.submit {
  text-align: right;
  padding: 60px;
  border-top: 1px solid #f5f5f5;
}
</style>
```



## 02-结算-渲染页面

> 目的：分离收货地址组件，渲染页面默认内容。



大致步骤：

- 分离收货地址组件
- 定义获结算信息API接口
- 页面组件获取数据，传入地址组件，渲染剩余内容
- 渲染地址组件



落的代码：

1. 分离收货地址组件

`src/member/pay/components/checkout-address.vue`  定义组件

```vue
<template>
  <div class="checkout-address">
    <div class="text">
      <!-- <div class="none">您需要先添加收货地址才可提交订单。</div> -->
      <ul>
        <li><span>收<i/>货<i/>人：</span>朱超</li>
        <li><span>联系方式：</span>132****2222</li>
        <li><span>收货地址：</span>海南省三亚市解放路108号物质大厦1003室</li>
      </ul>
      <a href="javascript:;">修改地址</a>
    </div>
    <div class="action">
      <XtxButton class="btn">切换地址</XtxButton>
      <XtxButton class="btn">添加地址</XtxButton>
    </div>
  </div>
</template>
<script>
export default {
  name: 'CheckoutAddress'
}
</script>
<style scoped lang="less">
.checkout-address {
  border: 1px solid #f5f5f5;
  display: flex;
  align-items: center;
  .text {
    flex: 1;
    min-height: 90px;
    display: flex;
    align-items: center;
    .none {
      line-height: 90px;
      color: #999;
      text-align: center;
      width: 100%;
    }
    > ul {
      flex: 1;
      padding: 20px;
      li {
        line-height: 30px;
        span {
          color: #999;
          margin-right: 5px;
          > i {
            width: 0.5em;
            display: inline-block;
          }
        }
      }
    }
    > a {
      color: @xtxColor;
      width: 160px;
      text-align: center;
      height: 90px;
      line-height: 90px;
      border-right: 1px solid #f5f5f5;
    }
  }
  .action {
    width: 420px;
    text-align: center;
    .btn {
      width: 140px;
      height: 46px;
      line-height: 44px;
      font-size: 14px;
      &:first-child {
        margin-right: 10px;
      }
    }
  }
}
</style>
```

`src/views/member/pay/checkout.vue`  使用组件

```diff
+import CheckoutAddress from './components/checkout-address'
export default {
  name: 'XtxPayCheckoutPage',
+  components: { CheckoutAddress }
}
```

```diff
        <!-- 收货地址 -->
        <h3 class="box-title">收货地址</h3>
        <div class="box-body">
+          <CheckoutAddress />
        </div>
```

原有结构和样式代码需要删除。



2. 定义获结算信息API接口

`src/api/order.js`   定义接口

```js
import request from '@/utils/request'

/**
 * 获取结算信息
 */
export const findCheckoutInfo = () => {
  return request('/member/order/pre', 'get')
}

```



3. 页面组件获取数据，传入地址组件，渲染剩余内容

`src/views/member/pay/checkout.vue`  获取数据

```diff
+import { findCheckoutInfo } from '@/api/order'
export default {
  name: 'XtxPayCheckoutPage',
  components: { CheckoutAddress },
  setup () {
+    const checkoutInfo = ref(null)
+    findCheckoutInfo().then(data => {
+      checkoutInfo.value = data.result
+    })
+    return { checkoutInfo }
  }
}
```

`src/views/member/pay/checkout.vue`  传入地址组件，地址列表

```diff
+      <div class="wrapper" v-if="checkoutInfo">
        <!-- 收货地址 -->
        <h3 class="box-title">收货地址</h3>
        <div class="box-body">
+          <CheckoutAddress :list="checkoutInfo.userAddresses" />
        </div>
```

`src/views/member/pay/checkout.vue`  渲染剩余内容

```vue
            <tbody>
              <tr v-for="item in checkoutInfo.goods" :key="item.id">
                <td>
                  <a href="javascript:;" class="info">
                    <img :src="item.picture" alt="">
                    <div class="right">
                      <p>{{item.name}}</p>
                      <p>{{item.attrsText}}</p>
                    </div>
                  </a>
                </td>
                <td>&yen;{{item.payPrice}}</td>
                <td>{{item.count}}</td>
                <td>&yen;{{item.totalPrice}}</td>
                <td>&yen;{{item.totalPayPrice}}</td>
              </tr>
            </tbody>
```

```vue
          <div class="total">
            <dl><dt>商品件数：</dt><dd>{{checkoutInfo.summary.goodsCount}}件</dd></dl>
            <dl><dt>商品总价：</dt><dd>¥{{checkoutInfo.summary.totalPrice}}</dd></dl>
            <dl><dt>运<i></i>费：</dt><dd>¥{{checkoutInfo.summary.postFee}}</dd></dl>
            <dl><dt>应付总额：</dt><dd class="price">¥{{checkoutInfo.summary.totalPayPrice}}</dd></dl>
          </div>
```



4. 渲染地址组件

`src/member/pay/components/checkout-address.vue`   

- 接收数据

```js
  props: {
    list: {
      type: Array,
      default: () => []
    }
  },
```

- 得到默认显示地址

```js
  setup (props) {
    // 显示的地址
    const showAddress = ref(null)
    if (props.list.length) {
      const defaultAddress = props.list.find(item => item.isDefault === 1)
      if (defaultAddress) {
        showAddress.value = defaultAddress
      } else {
        // eslint-disable-next-line vue/no-setup-props-destructure
        showAddress.value = props.list[0]
      }
    }
    return { showAddress }
  }
```

- 渲染组件

```vue
    <div class="text">
      <div v-if="!showAddress" class="none">您需要先添加收货地址才可提交订单。</div>
      <ul v-if="showAddress">
        <li><span>收<i/>货<i/>人：</span>{{showAddress.receiver}}</li>
        <li><span>联系方式：</span>{{showAddress.contact}}</li>
        <li><span>收货地址：</span>{{showAddress.fullLocation.replace(/ /g,'')+showAddress.address}}</li>
      </ul>
      <a v-if="showAddress" href="javascript:;">修改地址</a>
    </div>
```



## 03-结算-对话框组件封装

> 目的：实现一个对话框组件可设置标题，动态插入内容，动态插入底部操作按钮，打开关闭功能。

![1615279142371](./docs/media/1615279142371.png)



大致步骤：

- 参照xtx-confirm定义一个基础布局
- 实现设置标题
- 实现插入内容
- 实现插入底部操作按钮
- 实现打开关闭功能



落的代码：

1. 参照xtx-confirm定义一个基础布局

`src/components/library/xtx-dialog.vue`  定义组件

```vue
<template>
  <div class="xtx-dialog" :class="{fade}">
    <div class="wrapper" :class="{fade}">
      <div class="header">
        <h3>切换收货地址</h3>
        <a href="JavaScript:;" class="iconfont icon-close-new"></a>
      </div>
      <div class="body">
        对话框内容
      </div>
      <div class="footer">
        <XtxButton type="gray" style="margin-right:20px">取消</XtxButton>
        <XtxButton type="primary">确认</XtxButton>
      </div>
    </div>
  </div>
</template>
<script>
import { ref, onMounted } from 'vue'
export default {
  name: 'XtxDialog',
  setup () {
    const fade = ref(false)
    onMounted(() => {
      // 结构和样式同时加上无过度效果，需要些延时。
      setTimeout(() => {
        fade.value = true
      }, 0)
    })
    return { fade }
  }
}
</script>
<style scoped lang="less">
.xtx-dialog {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: 8887;
  background: rgba(0,0,0,0);
  &.fade {
    transition: all 0.4s;
    background: rgba(0,0,0,.5);
  }
  .wrapper {
    width: 600px;
    background: #fff;
    border-radius: 4px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-60%);
    opacity: 0;
    &.fade {
      transition: all 0.4s;
      transform: translate(-50%,-50%);
      opacity: 1;
    }
    .body {
      padding: 20px 40px;
      font-size: 16px;
      .icon-warning {
        color: @priceColor;
        margin-right: 3px;
        font-size: 16px;
      }
    }
    .footer {
      text-align: center;
      padding: 10px 0 30px 0;
    }
    .header {
      position: relative;
      height: 70px;
      line-height: 70px;
      padding: 0 20px;
      border-bottom: 1px solid #f5f5f5;
      h3 {
        font-weight: normal;
        font-size: 18px;
      }
      a {
        position: absolute;
        right: 25px;
        top: 25px;
        font-size: 24px;
        width: 20px;
        height: 20px;
        line-height: 20px;
        text-align: center;
        color: #999;
        &:hover {
          color: #666;
        }
      }
    }
  }
}
</style>
```

`src/views/member/pay/components/checkout-address.vue`  使用组件

```vue
<XtxDialog />
```

2. 实现设置标题

`src/components/library/xtx-dialog.vue`  定义组件

```js
  props: {
    title: {
      type: String,
      default: ''
    }
  },
```

```vue
      <div class="header">
        <h3>{{title}}</h3>
        <a href="JavaScript:;" class="iconfont icon-close-new"></a>
      </div>
```

`src/views/member/pay/components/checkout-address.vue`  使用组件

```vue
<XtxDialog title="切换收货地址" />
```

3. 实现插入内容

`src/components/library/xtx-dialog.vue`  定义组件

```diff
      <div class="body">
+        <slot />
      </div>
```

`src/views/member/pay/components/checkout-address.vue`  使用组件

```vue
<XtxDialog title="切换收货地址" >
  对话框内容
</XtxDialog>
```

4. 实现插入底部操作按钮

`src/components/library/xtx-dialog.vue`  定义组件

```diff
      <div class="footer">
+        <slot name="footer" />
      </div>
```

`src/views/member/pay/components/checkout-address.vue`  使用组件

```vue
    <XtxDialog title="切换收货地址">
      对话框内容
      <!-- vue3.0 仅支持v-slot+template写法 -->  
      <template v-slot:footer>
        <XtxButton type="gray" style="margin-right:20px">取消</XtxButton>
        <XtxButton type="primary">确认</XtxButton>
      </template>
    </XtxDialog>
```

5. 实现打开关闭功能
   1. 打开关闭通过v-model来实现
   2. 动画根据打开关闭状态来控制

`src/components/library/xtx-dialog.vue`  定义组件

```vue
<div class="xtx-dialog" :class="{fade}" v-show="visible">
```

```js
import { ref, watch } from 'vue'
export default {
  name: 'XtxDialog',
  props: {
    title: {
      type: String,
      default: ''
    },
    visible: {
      type: Boolean,
      default: false
    }
  },
  setup (props, { emit }) {
    const fade = ref(true)
    // 改造动画执行时机
    watch(() => props.visible, () => {
      setTimeout(() => {
        fade.value = props.visible
      }, 0)
    }, { immediate: true })
    // 关闭的时候通知父组件
    const close = () => {
      emit('update:visible', false)
    }
    return { fade, close }
  }
}
```

`src/views/member/pay/components/checkout-address.vue`  使用组件

```diff
    <div class="action">
+      <XtxButton @click="dialogVisible=true" class="btn">切换地址</XtxButton>
      <XtxButton class="btn">添加地址</XtxButton>
    </div>
+    <XtxDialog title="切换收货地址" v-model:visible="dialogVisible">
      对话框内容
      <template v-slot:footer>
+        <XtxButton @click="dialogVisible=false" type="gray" style="margin-right:20px">取消</XtxButton>
+        <XtxButton @click="dialogVisible=false" type="primary">确认</XtxButton>
      </template>
    </XtxDialog>
```

```js
    // 对话框显示隐藏
    const dialogVisible = ref(false)
    return { dialogVisible }
```



## 04-结算-收货地址-切换

> 目的：能够切换当前显示的地址，且通知结算组件当前地址ID用于提交订单使用。

![1617606875360](./docs/media/1617606875360.png)

大致步骤：

- 组件初始化的时候需要得到一个默认的地址ID通知给结算组件
- 对话框中渲染一个地址列表
- 实现可以选中的效果，点击确认后变更显示地址，通知结算组件地址ID



落地代码：

1. 组件初始化的时候需要得到一个默认的地址ID通知给结算组件

地址组件 `components/checkout-address.vue`

```diff
   // 对话框显示隐藏
    const dialogVisible = ref(false)
+    // 默认通知一个地址ID给父
+    emit('change', showAddress.value?.id)
    return { showAddress, dialogVisible }
```

```js
  // 1. 在拥有根元素的组件中，触发自定义事件，有没有emits选项无所谓
  // 2. 如果你的组件渲染的代码片段，vue3.0规范，需要在emits中申明你所触发的自定义事件
  // 3. 提倡：你发了自定义事件，需要在emits选项申明下，代码可读性很高
  emits: ['change'],
```

结算组件 `checkout.vue`

```js
    // 需要提交的字段
    const requestParams = reactive({
      addressId: null
    })
    // 切换地址
    const changeAddress = (id) => {
      requestParams.addressId = id
    }
    return { checkoutInfo, changeAddress }
```

```vue
<CheckoutAddress @change="changeAddress" :list="checkoutInfo.userAddresses" />
```

2. 对话框中渲染一个地址列表

地址组件 `components/checkout-address.vue`

```diff
    <XtxDialog title="切换收货地址" v-model:visible="dialogVisible">
+      <div class="text item" v-for="item in list" :key="item.id">
+        <ul>
+          <li><span>收<i/>货<i/>人：</span>{{item.receiver}}</li>
+          <li><span>联系方式：</span>{{item.contact}}</li>
+          <li><span>收货地址：</span>{{item.fullLocation.replace(/ /g,'')+item.address}}</li>
+        </ul>
+      </div>
      <template v-slot:footer>
```

```less
.xtx-dialog {
  .text {
    flex: 1;
    min-height: 90px;
    display: flex;
    align-items: center;
    &.item {
      border: 1px solid #f5f5f5;
      margin-bottom: 10px;
      cursor: pointer;
      &.active,&:hover {
        border-color: @xtxColor;
        background: lighten(@xtxColor,50%);
      }
      > ul {
        padding: 10px;
        font-size: 14px;
        line-height: 30px;
      }
    }
  }
}
```

3. 实现可以选中的效果，点击确认后变更显示地址，通知结算组件地址ID

地址组件 `components/checkout-address.vue`

```js
  // 对话框显示隐藏
    const dialogVisible = ref(false)
    // 打开对话框
    const openDialog = () => {
      dialogVisible.value = true
      selectedAddress.value = null
    }
    // 确认地址
    const confirmAddress = () => {
      dialogVisible.value = false
      showAddress.value = selectedAddress.value
      // 默认通知一个地址ID给父
      emit('change', showAddress.value?.id)
    }
    // 选择的地址
    const selectedAddress = ref(null)
    return { showAddress, dialogVisible, selectedAddress, openDialog, confirmAddress }
```

```diff
    <XtxDialog title="切换收货地址" v-model:visible="dialogVisible">
      <div
        class="text item"
+        :class="{active:selectedAddress&&item.id===selectedAddress.id}"
+        @click="selectedAddress=item"
        v-for="item in list"
        :key="item.id">
        <ul>
```

```vue
<XtxButton @click="openDialog()" class="btn">切换地址</XtxButton>
```

```vue
<XtxButton @click="confirmAddress()" type="primary">确认</XtxButton>
```



## 05-结算-收货地址-添加

> 目的：实现收货地址的添加。



大致步骤：

- 独立组件，准备一个对话框
- 完成表单布局
- 完成确认添加操作



落的代码：

1. 独立组件，准备一个对话框

`src/views/member/pay/components/address-edit.vue`   添加地址组件

```vue
<template>
  <XtxDialog title="添加收货地址" v-model:visible="dialogVisible">
    <div class="address-edit">
      表单
    </div>
    <template v-slot:footer>
      <XtxButton type="gray" style="margin-right:20px">取消</XtxButton>
      <XtxButton type="primary">确认</XtxButton>
    </template>
  </XtxDialog>
</template>
<script>
import { ref } from 'vue'
export default {
  name: 'AddressEdit',
  setup () {
    const dialogVisible = ref(false)
    // 打开函数
    const open = () => {
      dialogVisible.value = true
    }
    return { dialogVisible, open }
  }
}
</script>
<style scoped lang="less">
.address-edit {

}
</style>
```

`src/views/member/pay/components/checkout-address.vue`   使用添加地址组件

```diff
    // 添加收货地址组件
+   const addressEdit = ref(null)
+   const openAddressEdit = () => {
+     addressEdit.value.open()
+   }
    return {
      showAddress,
      dialogVisible,
      selectedAddress,
      openDialog,
      confirmAddress,
+      addressEdit,
+      openAddressEdit
    }
```

```vue
<XtxButton @click="openAddressEdit()" class="btn">添加地址</XtxButton>
```

2. 完成表单布局

`src/views/member/pay/components/address-edit.vue`   结构和样式

```vue
    <div class="xtx-form">
      <div class="xtx-form-item">
        <div class="label">收货人：</div>
        <div class="field">
          <input class="input" placeholder="请输入收货人" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">手机号：</div>
        <div class="field">
          <input class="input" placeholder="请输入手机号" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">地区：</div>
        <div class="field">
          <XtxCity placeholder="请选择所在地区"/>
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">详细地址：</div>
        <div class="field">
          <input class="input" placeholder="请输入详细地址" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">邮政编码：</div>
        <div class="field">
          <input class="input" placeholder="请输入邮政编码" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">地址标签：</div>
        <div class="field">
          <input class="input" placeholder="请输入地址标签，逗号分隔" />
        </div>
      </div>
    </div>
```

```less
.xtx-dialog {
  :deep(.wrapper){
    width: 780px;
    .body {
      font-size: 14px;
    }
  }
}
.xtx-form {
  padding: 0;
  input {
    outline: none;
    &::placeholder {
      color: #ccc;
    }
  }
}
.xtx-city {
  width: 320px;
  :deep(.select) {
    height: 50px;
    line-height: 48px;
    display: flex;
    padding: 0 10px;
    justify-content: space-between;
    .placeholder {
      color: #ccc;
    }
    i {
      color: #ccc;
      font-size: 18px;
    }
    .value {
      font-size: 14px;
    }
  }
  :deep(.option) {
    top: 49px;
  }
}
```

`src/components/library/xtx-city.vue`   暴露占位文字

```js
    placeholder: {
      type: String,
      default: '请选择配送地址'
    }
```

```vue
<span v-if="!fullName" class="placeholder">{{placeholder}}</span>
```



3. 完成确认添加操作

`src/views/member/pay/components/address-edit.vue`   动态绑定表单

```js
    // 表单数据
    const formData = reactive({
      receiver: '',
      contact: '',
      provinceCode: '',
      cityCode: '',
      countyCode: '',
      address: '',
      postalCode: '',
      addressTags: '',
      isDefault: 0,
      fullLocation: ''
    })
    // 选择地区
    const changeCty = (data) => {
      formData.provinceCode = data.provinceCode
      formData.cityCode = data.cityCode
      formData.countyCode = data.countyCode
      formData.fullLocation = data.fullLocation
    }
    return { dialogVisible, open, formData, changeCty }
```

```diff
    <div class="xtx-form">
      <div class="xtx-form-item">
        <div class="label">收货人：</div>
        <div class="field">
+          <input v-model="formData.receiver" class="input" placeholder="请输入收货人" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">手机号：</div>
        <div class="field">
+          <input v-model="formData.contact" class="input" placeholder="请输入手机号" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">地区：</div>
        <div class="field">
          <XtxCity
            placeholder="请选择所在地区"
+            :fullLocation="form.fullLocation"
+            @change="changeCty"
          />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">详细地址：</div>
        <div class="field">
+          <input  v-model="formData.address" class="input" placeholder="请输入详细地址" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">邮政编码：</div>
        <div class="field">
+          <input  v-model="formData.postalCode" class="input" placeholder="请输入邮政编码" />
        </div>
      </div>
      <div class="xtx-form-item">
        <div class="label">地址标签：</div>
        <div class="field">
+          <input v-model="formData.addressTags" class="input" placeholder="请输入地址标签，逗号分隔" />
        </div>
      </div>
    </div>
```

`src/api/order.js`  接口函数

```js
/**
 * 添加收货地址信息
 * @param {Object} address - 地址对象
 */
export const addAddress = (address) => {
  return request('/member/address', 'post', address)
}
```

`src/components/library/xtx-city.vue`  提供占位文字属性

```diff

    placeholder: {
      type: String,
      default: '请选择配送地区'
    }
```

```vue
<span class="placeholder" v-if="!fullLocation">{{placeholder}}</span>
```



`src/views/member/pay/components/address-edit.vue`   进行提交操作

```diff
    // 选择地区
    const changeCty = (data) => {
      formData.provinceCode = data.provinceCode
      formData.cityCode = data.cityCode
      formData.countyCode = data.countyCode
+      formData.fullLocation = data.fullLaction
    }
+    // 提交操作
+    const submit = () => {
+      addAddress(formData).then(data => {
+        // 添加成功
+        Message({ text: '添加收货地址成功', type: 'success' })
+        formData.id = data.result.id
+        dialogVisible.value = false
+        emit('on-success', formData)
+      })
+    }
+    return { dialogVisible, open, formData, changeCty, submit }
```

`src/views/member/pay/components/checkout-address.vue`   接受添加成功的地址对象

```diff
+    // 成功
+    const successHandler = (formData) => {
+      const json = JSON.stringify(formData)  // 需要克隆下，不然使用的是对象的引用
+      // eslint-disable-next-line vue/no-mutating-props
+      props.list.unshift(JSON.parse(json))
+    }
    return {
      showAddress,
      dialogVisible,
      selectedAddress,
      openDialog,
      confirmAddress,
      addressEdit,
      openAddressEdit,
+      successHandler
    }
```

```vue
    <!-- 添加地址 -->
    <AddressEdit ref="addressEdit" @on-success="successHandler" />
```

`src/views/member/pay/components/address-edit.vue`   每次打开对话框清空表单

```diff
    // 打开函数
    const open = (form) => {
      dialogVisible.value = true
+      // 传人{}的时候就是清空，否则就是赋值
+      for (const key in formData) {
+        formData[key] = form[key]
+      }
    }
```



## 06-结算-收货地址-修改

> 目的：在添加收货地址组件基础之上完成修改逻辑。



大致步骤：

- 打开对话框的时候传人当前需要修改的地址对象
- 再添加组件open函数处，接收数据赋值给表单，修改标题。
- 封装一个API接口函数实现修改，在提交事件中合并修改操作
- 父组件修改数据



落的代码：

1. 打开对话框的时候传人当前需需改的地址对象

`src/views/member/pay/checkout-address.vue`   

```vue
<a @click="openAddressEdit(showAddress)" v-if="showAddress" href="javascript:;">修改地址</a>
```



2. 再添加组件open函数处，接收数据赋值给表单，修改标题  

`src/views/member/pay/address-edit.vue`

```diff
    const formData = reactive({
+      id: '',
      receiver: '',
      contact: '',
      provinceCode: '',
      cityCode: '',
      countyCode: '',
+      fullLocation: '',
      address: '',
      postalCode: '',
      addressTags: '',
      isDefault: 0
    })
```

```vue
<XtxDialog :title="(formData.id?'编辑':'添加')+'收货地址'" v-model:visible="dialogVisible">
```

3. 封装一个API接口函数实现修改，在提交事件中合并修改操作

`src/api/order.js`

```js
/**
 * 编辑收货地址信息
 * @param {Object} address - 地址对象
 */
export const editAddress = (address) => {
  return request('/member/address', 'put', address)
}

```

`src/views/member/pay/address-edit.vue`

```js
    // 打开对话框函数
    const open = (address) => {
      // 先填充数据 - 编辑
      if (address.id) {
        for (const key in formData) {
          formData[key] = address[key]
        }
      } else {
        // 先清空数据 - 添加
        for (const key in formData) {
          if (key !== 'isDefault') {
            formData[key] = ''
          }
        }
      }
      dialogVisible.value = true
    }
```

```diff
    // 提交操作
    const app = getCurrentInstance()
    const submit = () => {
+      if (formData.id) {
+        editAddress(formData).then(data => {
+          // 修改成功
+          Message(app, { text: '修改收货地址成功', type: 'success' })
+          dialogVisible.value = false
+          emit('on-success', formData)
+        })
+      } else {
        addAddress(formData).then(data => {
          // 添加成功
          Message(app, { text: '添加收货地址成功', type: 'success' })
          formData.id = data.result.id
          dialogVisible.value = false
          emit('on-success', formData)
        })
+      }
    }
```



4. 父组件修改数据

`src/views/member/pay/components/checkout-address.vue`

```diff
    // 成功
    const successHandler = (formData) => {
+      const editAddress = props.list.find(item => item.id === formData.id)
+      if (editAddress) {
+        // 修改
+        for (const key in editAddress) {
+          editAddress[key] = formData[key]
+        }
+      } else {
        // 添加
        const json = JSON.stringify(formData) // 需要克隆下，不然使用的是对象的引用
        // eslint-disable-next-line vue/no-mutating-props
        props.list.unshift(JSON.parse(json))
+      }
```





## 07-结算-提交订单

> 目的：汇总提交订单需要的数据，进行提交。



大致步骤：

- 定义需要提交的数据对象
- 绑定提交订单点击事件，进行提交即可



落的代码：

1. 定义需要提交的数据对象

`src/views/member/pay/checkout.vue`

```diff
  setup () {
    const checkoutInfo = ref(null)
    findCheckoutInfo().then(data => {
      checkoutInfo.value = data.result
+      // 设置提交时候的商品
+      requestParams.goods = checkoutInfo.value.goods.map(item => {
+        return {
+          skuId: item.skuId,
+          count: item.count
+        }
+      })
    })
    // 需要提交的字段
    const requestParams = reactive({
      addressId: null,
+      deliveryTimeType: 1,
+      payType: 1,
+      buyerMessage: '',
+      goods: []
    })
```

2. 绑定提交订单点击事件，进行提交即可

`src/api/order.js`  提交订单API函数

```js
/**
 * 提交订单
 * @param {Object} order - 订单信息对象
 */
export const createOrder = (order) => {
  return request('/member/order', 'post', order)
}
```

`src/views/member/pay/checkout.vue`   提交订单

```vue
        <!-- 提交订单 -->
        <div class="submit">
          <XtxButton @click="submitOrder" type="primary">提交订单</XtxButton>
        </div>
```

```js
    // 提交订单
    const router = useRouter()
    const submitOrder = () => {
      if (!requestParams.addressId) return Message({ text: '请选择收货地址' })
      createOrder(requestParams).then(data => {
        router.push({ path: '/member/pay', query: { id: data.result.id } })
      })
    }
    return { checkoutInfo, changeAddress, submitOrder }
```





## 08-支付-支付页面-基础布局

> 目的：配置路由和支付页面基础布局。

![1615632580883](./docs/media/1615632580883.png)

`src/views/member/pay/index.vue`

```vue
<template>
  <div class="xtx-pay-page">
    <div class="container">
      <XtxBread>
        <XtxBreadItem to="/">首页</XtxBreadItem>
        <XtxBreadItem to="/cart">购物车</XtxBreadItem>
        <XtxBreadItem>支付订单</XtxBreadItem>
      </XtxBread>
      <!-- 付款信息 -->
      <div class="pay-info">
        <span class="icon iconfont icon-queren2"></span>
        <div class="tip">
          <p>订单提交成功！请尽快完成支付。</p>
          <p>支付还剩 <span>24分59秒</span>, 超时后将取消订单</p>
        </div>
        <div class="amount">
          <span>应付总额：</span>
          <span>¥5673.00</span>
        </div>
      </div>
      <!-- 付款方式 -->
      <div class="pay-type">
        <p class="head">选择以下支付方式付款</p>
        <div class="item">
          <p>支付平台</p>
          <a class="btn wx" href="javascript:;"></a>
          <a class="btn alipay" href="javascript:;"></a>
        </div>
        <div class="item">
          <p>支付方式</p>
          <a class="btn" href="javascript:;">招商银行</a>
          <a class="btn" href="javascript:;">工商银行</a>
          <a class="btn" href="javascript:;">建设银行</a>
          <a class="btn" href="javascript:;">农业银行</a>
          <a class="btn" href="javascript:;">交通银行</a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'XtxPayPage'
}
</script>
<style scoped lang="less">
.pay-info {
  background: #fff;
  display: flex;
  align-items: center;
  height: 240px;
  padding: 0 80px;
  .icon {
    font-size: 80px;
    color: #1dc779;
  }
  .tip {
    padding-left: 10px;
    flex: 1;
    p {
      &:first-child {
        font-size: 20px;
        margin-bottom: 5px;
      }
      &:last-child {
        color: #999;
        font-size: 16px;
      }
    }
  }
  .amount {
    span {
      &:first-child {
        font-size: 16px;
        color: #999;
      }
      &:last-child {
        color: @priceColor;
        font-size: 20px;
      }
    }
  }
}
.pay-type {
  margin-top: 20px;
  background-color: #fff;
  padding-bottom: 70px;
  p {
    line-height: 70px;
    height: 70px;
    padding-left: 30px;
    font-size: 16px;
    &.head {
      border-bottom: 1px solid #f5f5f5;
    }
  }
  .btn {
    width: 150px;
    height: 50px;
    border: 1px solid #e4e4e4;
    text-align: center;
    line-height: 48px;
    margin-left: 30px;
    color: #666666;
    display: inline-block;
    &.active,
    &:hover {
      border-color: @xtxColor;
    }
    &.alipay {
      background: url(https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/7b6b02396368c9314528c0bbd85a2e06.png) no-repeat center / contain;
    }
    &.wx {
      background: url(https://cdn.cnbj1.fds.api.mi-img.com/mi-mall/c66f98cff8649bd5ba722c2e8067c6ca.jpg) no-repeat center / contain;
    }
  }
}
</style>
```

`src/router/index.js`

```js
const PayIndex = () => import('@/views/member/pay/index')
```

```diff
      { path: '/member/checkout', component: PayCheckout },
+      { path: '/member/pay', component: PayIndex }
```



## 10-支付-支付页面-信息展示

> 目的：展示支付的订单相关信息。



大致步骤：

- 准备API接口函数获取订单详情
- 在组件获取数据渲染
- 完成倒计时效果



落的代码：



1. 准备API接口函数获取订单详情 `src/api/order.js`

```js
/**
 * 获取订单详情
 * @param {String} id - 订单ID
 */
export const findOrder = (id) => {
  return request('/member/order/' + id, 'get')
}
```

2. 在组件获取数据渲染  `src/views/component/pay/index.vue`

```js
import { ref } from 'vue'
import { findOrder } from '@/api/order'
import { useRoute } from 'vue-router'
export default {
  name: 'XtxPayPage',
  setup () {
    // 订单
    const order = ref(null)
    // 路由信息
    const route = useRoute()
    // 查询订单
    findOrder(route.query.id).then(data => {
      // 设置订单
      order.value = data.result
    })
    return { order }
  }
}
```
```diff
+    <div class="pay-info" v-if="order">
```

```diff
        <div class="amount">
          <span>应付总额：</span>
+          <span>¥{{order.payMoney}}</span>
        </div>
```

3. 完成倒计时效果

`src/hooks/index.js` 倒计时钩子函数封装

```js
// 提供复用逻辑的函数（钩子）
import { useIntersectionObserver, useIntervalFn } from '@vueuse/core'
import { ref, onUnmounted } from 'vue'
import dayjs from 'dayjs'
```

```js
/**
 * 支付倒计时函数
 */
export const usePayTime = () => {
  // 倒计时逻辑
  const time = ref(0)
  const timeText = ref('')
  const { pause, resume } = useIntervalFn(() => {
    time.value--
    timeText.value = dayjs.unix(time.value).format('mm分ss秒')
    if (time.value <= 0) {
      pause()
    }
  }, 1000, false)
  onUnmounted(() => {
    pause()
  })

  // 开启定时器 countdown 倒计时时间
  const start = (countdown) => {
    time.value = countdown
    timeText.value = dayjs.unix(time.value).format('mm分ss秒')
    resume()
  }

  return {
    start,
    timeText
  }
}
```

`src/views/member/pay/index.vue`  使用函数

```js
import { useRoute } from 'vue-router'
import { findOrderDetail } from '@/api/order'
import { ref } from 'vue'
import { usePayTime } from '@/hooks'

export default {
  name: 'XtxPayPage',
  setup () {
    // 根据地址栏ID发请求获取订单数据
    const route = useRoute()
    const order = ref(null)
    findOrderDetail(route.query.orderId).then(data => {
      order.value = data.result
      // 后端提供 countdown 倒计时秒数
      if (data.result.countdown > -1) {
        start(data.result.countdown)
      }
    })

    const { start, timeText } = usePayTime()

    return {
      order,
      timeText
    }
  }
}
```

```diff
        <div class="tip">
          <p>订单提交成功！请尽快完成支付。</p>
+          <p v-if="order.countdown > -1">支付还剩 <span>{{timeText}}</span>, 超时后将取消订单</p>
+          <p v-else>订单已经超时</p>
        </div>
```

## 11-支付-支付流程

> 目的：知道小兔鲜支付流程。



![1615641254875](./docs/media/1615641254875.png)



总结：

- PC前台点击支付按钮，新开标签页打开后台提供的支付链接带上订单ID还有回跳地址
- 后台服务发起支付，等待支付结果，修改订单状态，回跳PC前台结果页
- PC前台在结果页获取回跳URL参数订单ID查询支付状态，展示支付结果

```yaml
# 支付地址回调地址（可变）
http://www.corho.com:8080/#/pay/callback
```



测试：如果使用客户端需要下载 `沙箱支付宝` 开放平台扫码下载。

```
买家账号jfjbwb4477@sandbox.com
登录密码111111
支付密码111111
```





## 12-支付-跳转支付

> 目的：支付打开新页，当前页打开提示框。



1. 准备支付跳转链接

`src/utils/request.js`

```js
export const baseURL = 'http://pcapi-xiaotuxian-front-devtest.itheima.net/'
```

`src/views/member/pay/index.vue`

```js
    // 支付地址
    // const payUrl = '后台服务基准地址+支付页面地址+订单ID+回跳地址'
    const redirect = encodeURIComponent('http://www.corho.com:8080/#/pay/callback')
    const payUrl = `${baseURL}pay/aliPay?orderId=${route.query.orderId}&redirect=${redirect}`

    return { order, countdownText, payUrl }
```

```vue
<a class="btn alipay" :href="payUrl" target="_blank"></a>2.
```

2. 等待弹窗

![1615640280556](./docs/media/1615640280556.png)

 `src/views/component/pay/index.vue`

```vue
    <XtxDialog title="正在支付..." v-model:visible="visibleDialog">
      <div class="pay-wait">
        <img src="@/assets/images/load.gif" alt="">
        <div v-if="order">
            <p>如果支付成功：</p>
            <RouterLink :to="`/member/order/${order.id}`">查看订单详情></RouterLink>
            <p>如果支付失败：</p>
            <RouterLink to="/">查看相关疑问></RouterLink>
        </div>
      </div>
    </XtxDialog>
```

```js
    // 支付提示
    const visibleDialog = ref(false)
    return { order, timeText, visibleDialog }
```

```less
.pay-wait {
  display: flex;
  justify-content: space-around;
  p {
    margin-top: 30px;
    font-size: 14px;
  }
  a {
    color: @xtxColor;
  }
}
```







## 13-支付-结果展示

> 目的：准备一个支付完成的回调页面，展示支付后订单状态。

![1617520044257](./docs/media/1617520044257.png)

大致步骤：

- 准备一个基础页面
- 根据地址订单ID查询订单状态进行展示，或者是地址栏支付结果。



落的代码：



1. 准备一个基础页面

```vue
<template>
  <div class="xtx-pay-page">
    <div class="container">
      <XtxBread>
        <XtxBreadItem to="/">首页</XtxBreadItem>
        <XtxBreadItem to="/cart">购物车</XtxBreadItem>
        <XtxBreadItem>支付结果</XtxBreadItem>
      </XtxBread>
      <!-- 支付结果 -->
      <div class="pay-result">
        <span class="iconfont icon-queren2 green"></span>
        <!-- <span class="iconfont icon-shanchu red" ></span> -->
        <p class="tit">订单支付成功</p>
        <p class="tip">我们将尽快为您发货，收货期间请保持手机畅通</p>
        <p>支付方式：<span>微信支付</span></p>
        <p>支付金额：<span>¥1899.00</span></p>
        <div class="btn">
          <XtxButton type="primary" style="margin-right:20px">查看订单</XtxButton>
          <XtxButton type="gray">进入首页</XtxButton>
        </div>
        <p class="alert">
          <span class="iconfont icon-tip"></span>
          温馨提示：小兔鲜儿不会以订单异常、系统升级为由要求您点击任何网址链接进行退款操作，保护资产、谨慎操作。
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'XtxPayResultPage'
}
</script>
<style scoped lang="less">
.pay-result {
  padding: 100px 0;
  background: #fff;
  text-align: center;
  > .iconfont {
    font-size: 100px;
  }
  .green {
    color: #1dc779;
  }
  .red {
    color: @priceColor;
  }
  .tit {
    font-size: 24px;
  }
  .tip {
    color: #999;
  }
  p {
    line-height: 40px;
    font-size: 16px;
  }
  .btn {
    margin-top: 50px;
  }
  .alert {
    font-size: 12px;
    color: #999;
    margin-top: 50px;
  }
}
</style>
```

2. 根据地址订单ID查询订单状态进行展示

````vue
<template>
  <div class="xtx-pay-page">
    <div class="container">
      <XtxBread>
        <XtxBreadItem to="/">首页</XtxBreadItem>
        <XtxBreadItem to="/cart">购物车</XtxBreadItem>
        <XtxBreadItem>支付结果</XtxBreadItem>
      </XtxBread>
      <!-- 支付结果 -->
      <div class="pay-result" v-if="order">
        <span v-if="$route.query.payResult" class="iconfont icon-queren2 green"></span>
        <span v-else class="iconfont icon-shanchu red" ></span>
        <p class="tit">订单支付{{$route.query.payResult?'成功':'失败'}}</p>
        <p class="tip">我们将尽快为您发货，收货期间请保持手机畅通</p>
        <p>支付方式：<span>支付宝支付</span></p>
        <p>支付金额：<span class="red">¥{{order.payMoney}}</span></p>
        <div class="btn">
          <XtxButton @click="$router.push('/member/order')" type="primary" style="margin-right:20px">查看订单</XtxButton>
          <XtxButton @click="$router.push('/')" type="gray">进入首页</XtxButton>
        </div>
        <p class="alert">
          <span class="iconfont icon-tip"></span>
          温馨提示：小兔鲜儿不会以订单异常、系统升级为由要求您点击任何网址链接进行退款操作，保护资产、谨慎操作。
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import { ref } from 'vue'
import { findOrderDetail } from '@/api/order'
import { useRoute } from 'vue-router'
export default {
  name: 'XtxPayResultPage',
  setup () {
    const order = ref(null)
    const route = useRoute()
    findOrderDetail(route.query.orderId).then(data => {
      order.value = data.result
    })
    return { order }
  }
}
</script>
<style scoped lang="less">
.pay-result {
  padding: 100px 0;
  background: #fff;
  text-align: center;
  > .iconfont {
    font-size: 100px;
  }
  .green {
    color: #1dc779;
  }
  .red {
    color: @priceColor;
  }
  .tit {
    font-size: 24px;
  }
  .tip {
    color: #999;
  }
  p {
    line-height: 40px;
    font-size: 16px;
  }
  .btn {
    margin-top: 50px;
  }
  .alert {
    font-size: 12px;
    color: #999;
    margin-top: 50px;
  }
}
</style>

````











