# api-integration

## 功能说明

封装 API 调用，提供统一的请求/响应处理，支持拦截器和错误处理。

## 请求规范

### 基础请求封装

```javascript
// services/request.js
const BASE_URL = 'https://api.example.com'

export function request(options) {
  return new Promise((resolve, reject) => {
    uni.request({
      url: BASE_URL + options.url,
      method: options.method || 'GET',
      data: options.data || {},
      header: {
        'Content-Type': 'application/json',
        ...options.header
      },
      success: (res) => {
        if (res.statusCode === 200) {
          resolve(res.data)
        } else {
          reject(res)
        }
      },
      fail: reject
    })
  })
}
```

### API 服务模块化

```javascript
// services/user.js
import { request } from './request'

export const userApi = {
  login(data) {
    return request({
      url: '/api/login',
      method: 'POST',
      data
    })
  },
  getUserInfo(id) {
    return request({
      url: `/api/users/${id}`,
      method: 'GET'
    })
  }
}
```

## 响应规范

```javascript
// 统一响应格式
{
  "code": 0,        // 0=成功，非0=失败
  "data": {},       // 数据
  "message": ""     // 消息
}
```

## 必须遵守的约束

1. **错误处理**: 所有请求必须包含 `.catch()` 处理
2. **loading 状态**: 发起请求时显示 loading，完成后隐藏
3. **Token 处理**: 统一在请求头携带 Authorization
4. **超时设置**: 默认 30 秒超时

## 推荐模板

```javascript
// 统一错误处理
uni.showToast({
  title: '网络请求失败',
  icon: 'none'
})
```
