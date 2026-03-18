# figma-to-code

## 功能说明

使用 Figma 设计稿转换为 uni-app 代码，支持页面结构和样式提取。

## 转换流程

1. **Figma 获取**: 从 Figma 导出设计稿信息
2. **结构分析**: 解析图层结构识别组件层级
3. **代码生成**: 生成符合 uni-app 规范的 Vue 文件
4. **样式转换**: 将 Figma 样式转换为 CSS/SCSS

## Figma 节点信息获取

```javascript
{
  name: "组件名称",
  type: "COMPONENT" | "FRAME" | "GROUP",
  children: [...],
  absoluteBoundingBox: {
    x: 0,
    y: 0,
    width: 375,
    height: 812
  },
  fills: [...],
  strokes: [...],
  effects: [...]
}
```

## 转换规范

### 容器转换

| Figma | uni-app |
|-------|---------|
| Frame | view |
| Group | view (加 flex 布局) |
| Component | component |

### 文本转换

| Figma 属性 | CSS 属性 |
|-----------|---------|
| fontFamily | font-family |
| fontSize | font-size |
| fontWeight | font-weight |
| letterSpacing | letter-spacing |
| lineHeightPx | line-height |

### 颜色转换

```javascript
// RGBA 转 hex
const toHex = (r, g, b, a) => {
  const alpha = Math.round((a || 1) * 255)
  return `#${[r, g, b].map(x => x.toString(16).padStart(2, '0')).join('')}${alpha.toString(16).padStart(2, '0')}`
}
```

## 约束

1. **图片资源**: 导出为 base64 或下载到 static 目录
2. **布局方式**: 默认使用 flex 布局
3. **单位转换**: Figma px 需除以 2 适配 dpr
4. **层级处理**: 使用 v-if 控制显隐，避免 z-index 复杂化

## 工具使用

使用 `Framelink MCP for Figma` 工具获取设计稿数据:

```javascript
mcp__Framelink_MCP_for_Figma__get_figma_data({
  fileKey: "xxx",
  nodeId: "xxx"
})
```
