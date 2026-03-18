# component-builder

## 功能说明

封装符合 uni-app 规范的业务组件，支持 props、events、slots 等特性。

## 组件结构规范

```
components/
└── MyComponent/
    ├── index.vue          # 主组件文件
    ├── index.scss         # 组件样式（可选）
    └── props.js           # Props 定义（可选）
```

## 必须遵守的约束

### Props 规范

```javascript
export default {
  props: {
    // 基础类型
    title: {
      type: String,
      default: ''
    },
    // 复杂类型
    items: {
      type: Array,
      default: () => []
    },
    // 必填
    value: {
      type: Number,
      required: true
    }
  }
}
```

### 组件事件规范

```javascript
methods: {
  handleClick() {
    this.$emit('update', this.value)
    this.$emit('change', { id: 1 })
  }
}
```

### 插槽规范

```vue
<slot name="header" />
<slot />
<slot name="footer" />
```

## 组件注册

全局组件需在 `pages.json` 的 `easycom` 中配置:

```json
{
  "easycom": {
    "autoscan": true,
    "custom": {
      "^my-(.*)": "@/components/my-$1/index.vue"
    }
  }
}
```

## 命名规范

- 组件名: `MyComponent` (PascalCase)
- 使用时: `<MyComponent />` 或 `<my-component />`
