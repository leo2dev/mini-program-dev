# uni-app-init

## 功能说明

项目脚手架创建，生成符合规范的 uni-app 项目结构，支持多端配置。

## 目录结构规范

```
src/
├── pages/                    # 页面目录
│   └── index/
│       └── index.vue
├── static/                   # 静态资源
├── components/                # 组件目录
├── utils/                    # 工具函数
├── services/                 # API 服务
├── store/                    # 状态管理
├── styles/                   # 全局样式
│   └── common.scss
├── App.vue                   # 应用入口
├── main.js                   # 主入口
└── manifest.json             # 应用配置
```

## 必须遵守的约束

1. **页面文件**: 每个页面必须有独立目录，包含 `.vue` 文件
2. **组件注册**: 全局组件需在 `easycom` 中配置
3. **静态资源**: 仅放 `static/` 目录，其他路径不打包
4. **命名规范**: 页面/组件名使用 kebab-case

## 多端配置规范

`manifest.json` 必须包含:

```json
{
  "mp-weixin": {
    "appid": "",
    "setting": {
      "urlCheck": false,
      "es6": true
    }
  },
  "h5": {
    "router": {
      "base": "./"
    }
  }
}
```

## 推荐模板

- 使用 `easycom` 模式自动导入组件
- 采用 `scss` 预处理器
- 启用 `async` 函数支持
