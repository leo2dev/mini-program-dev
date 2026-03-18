# page-generator

## 功能说明

根据描述生成页面代码，自动注册路由，生成符合 uni-app 规范的页面文件。

## 必须遵守的约束

### pages.json 规范

```json
{
  "pages": [
    {
      "path": "pages/index/index",
      "style": {
        "navigationBarTitleText": "首页",
        "enablePullDownRefresh": false
      }
    }
  ],
  "globalStyle": {
    "navigationBarTextStyle": "black",
    "navigationBarTitleText": "uni-app",
    "navigationBarBackgroundColor": "#F8F8F8",
    "backgroundColor": "#F8F8F8"
  }
}
```

### 页面模板

```vue
<template>
  <view class="container">
    <!-- 页面内容 -->
  </view>
</template>

<script>
export default {
  data() {
    return {}
  },
  onLoad(options) {
    // 页面加载
  },
  methods: {
    // 方法
  }
}
</script>

<style lang="scss" scoped>
.container {
  // 样式
}
</style>
```

## 自动注册规则

1. 生成页面后自动追加到 `pages.json` 的 `pages` 数组
2. 使用 `uni.navigateTo` / `uni.switchTab` 进行页面跳转
3. 页面路径必须与目录结构一致

## 命名规范

- 页面目录: `src/pages/{page-name}/`
- 页面文件: `src/pages/{page-name}/{page-name}.vue`
- 路由路径: `pages/{page-name}/{page-name}`
