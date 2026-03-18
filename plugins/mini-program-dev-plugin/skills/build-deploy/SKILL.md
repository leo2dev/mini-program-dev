# build-deploy

## 功能说明

多端构建与发布，支持微信小程序、H5 等平台的构建配置与发布流程。

## 环境配置规范

### 多环境变量

```javascript
// environment/index.js
const env = process.env.NODE_ENV

const envConfig = {
  development: {
    baseUrl: 'http://localhost:3000',
    apiPrefix: '/api'
  },
  production: {
    baseUrl: 'https://api.production.com',
    apiPrefix: '/api'
  }
}

export default envConfig[env] || envConfig.development
```

### package.json scripts

```json
{
  "scripts": {
    "dev:mp-weixin": "uni -p mp-weixin",
    "build:mp-weixin": "uni build -p mp-weixin",
    "dev:h5": "uni",
    "build:h5": "uni build",
    "build:all": "npm run build:mp-weixin && npm run build:h5"
  }
}
```

## 构建流程

### 微信小程序发布

1. 运行 `npm run build:mp-weixin`
2. 打开微信开发者工具
3. 导入 `dist/dev/mp-weixin` 目录
4. 检查无警告后提交审核

### H5 发布

1. 运行 `npm run build:h5`
2. 部署 `dist/build/h5` 目录到服务器
3. 配置 SPA 路由 fallback

## 必须遵守的约束

1. **代码检查**: 构建前运行 ESLint 检查
2. **环境隔离**: 不同环境使用不同 API 地址
3. **版本号**: 发布前更新 `manifest.json` 版本
4. **分包加载**: 大型应用启用分包配置

## 分包配置示例

```json
{
  "pages": [...],
  "subPackages": [
    {
      "root": "pages-sub/",
      "pages": [...]
    }
  ]
}
```
