## Text 文本 <to-api/>

<demo-model url="/pages/componentsC/link/index"></demo-model>

此组件集成了文本类在项目中的常用功能，包括状态，拨打电话，格式化日期，*替换，超链接...等功能。
您大可不必在使用特殊文本时自己定义，text组件几乎涵盖您能使用的大部分场景。

### 平台差异说明

|App|H5|微信小程序|支付宝小程序|百度小程序|头条小程序|QQ小程序|
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|√|√|√|√|√|√|√|

### 基本使用

- 通过`text`参数设置文本内容。推荐您使用`:text='value'`的形式

```html
<u--text text="我用十年青春,赴你最后之约"></u--text>
```
### 设置主题

- 通过`type`参数设置文本主题，我们提供了五类属性。
- `primary  error  success  warning  info`

```html
<u--text type="primary" text="主色"></u--text>
<u--text type="error"   text="错误"></u--text>
<u--text type="success" text="成功"></u--text>
<u--text type="warning" text="警告"></u--text>
<u--text type="info"    text="信息"></u--text>
```
### 拨打电话

- 通过将`mode`属性设置为`phone`即可调用拨打电话，提供加密值`encrypt`
- 除此之外还有格式化日期，姓名脱敏，超链接，千分位金额等属性，将在以下实例中展示

```html
<u--text mode="phone" text="15019479320" encrypt></u--text>
```

### 日期格式化

```html
<u--text mode="date" text="1612959739"></u--text>
```
### 姓名脱敏

```html
<u--text mode="name" text="张**"></u--text>
```

### 超链接
添加`href`指定链接地址

```html
<u--text mode="link" text="Go to uView docs" href="https://www.uviewui.com" ></u--text>
```
### 显示金额

```html
<u--text mode="price" text="728732.32"></u--text>
```
### 前后图标
添加`prefixIcon,suffixIcon`指定图标和位置，`iconStyle`设置图标大小
```html
<u--text prefixIcon="baidu" iconStyle="font-size: 19px" text="百度一下,你就知道"></u--text>
<u--text suffixIcon="arrow-leftward" iconStyle="font-size: 18px" text="查看更多"></u--text>
```

### 超出隐藏
内置了文字超出隐藏样式，设置`lines`属性表明几行后隐藏
```html
<u--text :lines="2" text="关于uView的取名来由，首字母u来自于uni-app首字母，
uni-app是基Vuejs，Vue和View(延伸为UI、视图之意)同音，同时view组件uni-app中
最础最重要的组件，故取名uView，表达源于uni-app和Vue之意，同时在此也对它示感谢。"></u--text>
```

### 小程序开放能力
针对小程序开放能力，我们提供了分享，请在小程序环境下使用
```html
<u--text text="分享到微信" openType="share" type="success" @click="clickHandler"></u--text>
<script>
	export default {
		onLoad() {},
		methods: {
			clickHandler() {
				// #ifndef MP-WEIXIN
				uni.$u.toast('请在微信小程序内查看效果')
				// #endif
			}
		},
	}
</script>
```

### API

### List Props

| 参数          | 说明            | 类型            | 默认值             |  可选值   |
|-------------  |---------------- |---------------|------------------ |-------- |
| type | 主题颜色 | String | - | - |
| show | 是否显示 | Boolean | true | false |
| text | 显示的值 | String \| Number  | - | - |
| prefixIcon | 前置图标 | String | - | - |
| suffixIcon | 后置图标 | String | - | - |
| mode | 文本处理的匹配模式 | String | - | text-普通文本，price-价格，phone-手机号，name-姓名，date-日期，link-超链接 |
| href | mode=link下，配置的链接 | String | - | - |
| format | 格式化规则 | String \| Function  | - | - |
| call | mode=phone时，点击文本是否拨打电话 | Boolean  | false | true |
| encrypt | 是否对mode=phone|name类型文本进行脱敏，用*号替换部分文本 | Boolean  | false | - |
| openType | 小程序的打开方式 | String  | - | - |
| bold | 是否粗体，默认normal | Boolean | false | true |
| block | 是否块状 | Boolean | false | true |
| lines | 文本显示的行数，如果设置，超出此行数，将会显示省略号 | String \| Number | - | - |
| color | 文本颜色 | String | #303133 | - |
| size | 字体大小 | String \| Number | 15 | - |
| iconStyle | 图标的样式 | Object \| String | 15px | - |
| precision | 是否显示金额的千分位，mode=price时有效 | Boolean | true | false |
| decoration | 文字装饰，下划线，中划线等 | String | none | underline、line-through |
| margin | 外边距，对象、字符串，数值形式均可 | Object \| Number \| String | - | - |
| lineHeight | 文本行高 | Number \| String | - | - |
| align | 文本对齐方式 | String | left | center、right |
| wordWrap | 文字换行 | String | normal | break-word、anywhere |


### List Events

|事件名|说明|回调参数|
|:-|:-|:-|:-|
| click | 点击触发事件 | - |

