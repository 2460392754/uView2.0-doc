## Skeleton 骨架屏 <to-api/>

<demo-model url="/pages/componentsC/skeleton/skeleton"></demo-model>


骨架屏一般用于页面在请求远程数据尚未完成时，页面用灰色块预显示本来的页面结构，给用户更好的体验。  


::: tip 说明
由于```VUE```和```NVUE```的特性不同，组件动画在```VUE```上为由左到右形式，在```NVUE```上为明暗显隐的形式。
:::

### 平台差异说明

|App|H5	|微信小程序	|支付宝小程序		|百度小程序	|头条小程序	|QQ小程序	|
|:-:|:-:|:-:		|:-:			|:-:		|:-:		|:-:		|
|√	|√	|√			|√				|√			|√			|√			|

### 基本使用

组件由```标题```，```段落```和```头像```组件组件，其中```段落```需要通过```rows```参数配置才显示，可以通过```title```和```avatar```是否显示```标题```和```头像``` 。  
该组件的使用，有几个需要注意的点，如下：
- `title`(可选)，是否显示```标题```占位行，该占位行不布满全屏宽度，同时与```段落```的距离较大以做明显区分
- `avatar`(可选)，是否在左上角位置显示圆形的```头像```占位区域
- `rows`(可选)，```段落```的行数
- `loading`(必选)，是否加载中状态，如果为`true```则显示骨架屏组件占位，否则显示插槽中的内容

数据请求完成后，将`loading`设置为`false`，会隐藏骨架组件

```html
<template>
	<u-skeleton
	    rows="3"
	    title
		loading
	></u-skeleton>
</template>
```

### 加载中动画

设置`animate`为`true`，加载中的骨架块将会有一个动画效果，用以加强视觉效果。

```html
<u-skeleton :loading="true" :animate="true"></u-skeleton>
```

### 显示头像
```html
<u-skeleton :loading="true" avatar rows="1"></u-skeleton>
```

### 插槽内容

可以通过插槽写入展示的内容，当请求结束，将```loading```设置为```false```，此时会隐藏骨架组件，同时展示插槽内容。

```html
<template>
	<u-skeleton
	    rows="2"
		:loading="loading"
		avatar
		:title="false"
	>
		<u--text>loading为false时，将会展示此处插槽内容</u--text>
	</u-skeleton>
</template>

<script>
	export default {
		data() {
			return {
				loading: true
			}
		},
		onLoad() {
			// 延时2秒钟
			uni.$u.sleep(2000).then(() => {
				this.loading = false
			})
		}
	}
</script>
```

### 演示项目完整代码
:::demo 演示项目完整代码
```html
<template>
	<view class="u-page">
		<view class="u-demo-block">
			<text class="u-demo-block__title">基础使用</text>
			<view class="u-demo-block__content">
				<u-skeleton
					rows="3"
					title
					loading
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">自定义段落行数</text>
			<view class="u-demo-block__content">
				<u-skeleton
					rows="2"
					title
					loading
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">设置段落宽度</text>
			<view class="u-demo-block__content">
				<u-skeleton
					rows="2"
					title
					:rowsWidth="['100%', '35%']"
					loading
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">设置段落高度</text>
			<view class="u-demo-block__content">
				<u-skeleton
					rows="3"
					title
					:rowsWidth="['100%', '100%', '100%']"
					:rowsHeight="['18px', '18px', '80px']"
					loading
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">是否开启动画</text>
			<u-switch
				v-model="switch1"
				space="2"
				inactiveColor="#e6e6e6"
			></u-switch>
			<u-gap
				height="15"
				bgColor="#fff"
			></u-gap>
			<view class="u-demo-block__content">
				<u-skeleton
					:animate="switch1"
					rows="3"
					title
					loading
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">展示头像</text>
			<u-gap
				height="15"
				bgColor="#fff"
			></u-gap>
			<view class="u-demo-block__content">
				<u-skeleton
					:animate="switch1"
					rows="3"
					title
					loading
					avatar
				></u-skeleton>
			</view>
		</view>
		<view class="u-demo-block">
			<text class="u-demo-block__title">切换状态</text>
			<u-switch
				v-model="switch2"
				space="2"
				inactiveColor="#e6e6e6"
			></u-switch>
			<u-gap
				height="15"
				bgColor="#fff"
			></u-gap>
			<view class="u-demo-block__content">
				<u-skeleton
					rows="2"
					title
					:loading="switch2"
					avatar
					rowsHeight="14"
				>
					<view class="u-skeleton-slot">
						<image
							src="/static/uview/common/logo.png"
							class="u-skeleton-slot__image"
						></image>
						<view class="u-skeleton-slot__content">
							<u--text
								text="利剑出鞘,一统江湖"
								type="main"
								size="16"
							></u--text>
							<u--text
								type="tips"
								size="14"
								customStyle="margin-top: 5px"
								text="众多组件覆盖开发过程的各个需求，组件功能丰富，多端兼容。让您快速集成，开箱即用"
							></u--text>
						</view>
					</view>
				</u-skeleton>
			</view>
			<view
				class=""
				style="height: 50px;"
			>

			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				switch1: true,
				switch2: false
			}
		}
	}
</script>

<style lang="scss">
	.u-skeleton-slot {
		@include flex;
		align-items: flex-start;

		&__image {
			width: 40px;
			height: 40px;
			border-radius: 100px;
		}

		&__content {
			margin-left: 10px;
			flex: 1;
		}
	}
</style>

```
:::

### API

### Props

| 参数			| 说明																				| 类型								| 默认值	|  可选值	|
|:-				|:-																					|:-									|:-		|:-			|
| loading		| 是否显示骨架占位图，设置为`false`将会展示子组件内容									| Boolean							| true	| false		|
| animate		| 是否开启动画效果																	| Boolean							| true	| false		|
| rows			| 段落占位图行数																		| Number &#124; String				| 0		| -			|
| rowsWidth		| 段落占位图的宽度，可以为百分比，数值，带单位字符串等，可通过数组传入指定每个段落行的宽度	| String &#124; Array &#124; Number	| 100%	| -			|
| rowsHeight	| 段落的高度																			| String &#124; Array &#124; Number | 18	| -			|
| title			| 是否展示标题占位图																	| Boolean							| true	| false		|
| titleWidth	| 标题的宽度																			| String &#124; Number				| 50%	| -			|
| titleHeight	| 标题的高度																			| String &#124; Number				| 18	| -			|
| avatar		| 是否展示头像占位图																	| Boolean							| false	| true		|
| avatarSize	| 头像占位图大小																		| String &#124; Number				| 32	| -			|
| avatarShape	| 头像占位图的形状，circle-圆形，square-方形											| String							| circle| square	|

