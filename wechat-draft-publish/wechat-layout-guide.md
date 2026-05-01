# 微信公众号排版兼容规范

## 核心原则
微信公众号编辑器会大量过滤CSS，排版必须遵循以下规则才能正常显示。

## ❌ 会被过滤/不支持的
- `<style>` 标签和 class 选择器
- 深色背景主题（`background-color: #0a0e17` 等深色）
- CSS3 高级特性：flex、grid、box-shadow、text-shadow、transform、position、opacity、backdrop-filter
- 外部图片URL（必须是 `mmbiz.qpic.cn` 域名）
- JavaScript 和 `<script>` 标签
- `<html><head><body>` 外层标签（只需输出body片段）

## ✅ 支持的样式
- **内联样式**：所有样式必须写在 `style="..."` 里
- **支持的CSS属性**：color, font-size, font-weight, text-align, line-height, margin, padding, border, background-color（浅色）, border-radius, letter-spacing
- **标签**：`<section>`, `<p>`, `<span>`, `<strong>`, `<em>`, `<br>`, `<img>`, `<a>`

## 推荐配色方案

```
品牌主色：#1a73e8（科技蓝）
辅助色：#ff6b35（活力橙，强调用）
正文字色：#333333
次要文字：#666666 / #999999
背景色：白色为主
引用背景：#f7f8fa
互动框背景：#e8f0fe
分割线：#eeeeee
```

## 排版模块模板

### 1. 标题区
```html
<section style="text-align:center;margin-bottom:20px;">
  <span style="font-size:24px;font-weight:bold;color:#1a73e8;line-height:1.4;">文章标题</span>
</section>
<section style="text-align:center;margin-bottom:30px;">
  <span style="font-size:14px;color:#999999;">作者 · 日期</span>
</section>
```

### 2. 小标题
```html
<section style="margin-top:30px;margin-bottom:16px;padding-left:12px;border-left:3px solid #1a73e8;">
  <span style="font-size:18px;font-weight:bold;color:#333333;line-height:1.6;">小标题文字</span>
</section>
```

### 3. 正文段落
```html
<section style="margin-bottom:20px;">
  <span style="font-size:16px;color:#333333;line-height:1.8;">正文内容</span>
</section>
```

### 4. 引用/金句
```html
<section style="margin:20px 0;padding:16px 18px;background-color:#f7f8fa;border-left:3px solid #1a73e8;border-radius:0 6px 6px 0;">
  <span style="font-size:15px;color:#333333;line-height:1.8;font-style:italic;">引用内容</span>
</section>
```

### 5. 强调文字
```html
<strong style="color:#ff6b35;">关键词</strong>
<strong style="color:#1a73e8;">数据/术语</strong>
```

### 6. 图片 + 图注
```html
<section style="margin:25px 0;text-align:center;">
  <img src="微信图片URL" style="width:100%;border-radius:6px;"/>
  <p style="font-size:12px;color:#999999;margin-top:8px;text-align:center;">图注说明</p>
</section>
```

### 7. 互动引导框
```html
<section style="margin-top:30px;padding:20px;background-color:#e8f0fe;border-radius:8px;text-align:center;">
  <span style="font-size:16px;color:#1a73e8;font-weight:bold;line-height:1.8;">互动引导语</span>
</section>
```

### 8. 卡片式链接
```html
<section style="margin-top:30px;padding-top:20px;border-top:1px solid #eeeeee;">
  <span style="font-size:15px;color:#1a73e8;font-weight:bold;">📎 延伸阅读</span>
</section>

<section style="margin-top:12px;padding:14px 16px;background-color:#f7f8fa;border-left:3px solid #1a73e8;border-radius:0 6px 6px 0;margin-bottom:8px;">
  <span style="font-size:14px;color:#333333;line-height:1.6;"><strong style="color:#1a73e8;">链接名称</strong></span><br/>
  <span style="font-size:12px;color:#999999;line-height:1.4;">简短描述</span><br/>
  <span style="font-size:12px;color:#1a73e8;line-height:1.4;">域名简写</span>
</section>
```

### 9. 数据卡片
```html
<section style="padding:16px;background-color:#f7f8fa;border-radius:6px;margin:15px 0;text-align:center;">
  <span style="font-size:28px;font-weight:bold;color:#1a73e8;">87%</span><br/>
  <span style="font-size:13px;color:#666666;">WebVoyager成功率</span>
</section>
```

## 重要提醒
1. **图片URL必须先用uploadimg接口上传**，获取 `mmbiz.qpic.cn` 域名URL
2. **中文不要Unicode转义**：API调用时用 `ensure_ascii=False`
3. **HTML只输出body片段**，不带外层标签
4. **微信会去除JS和外部链接**，`<a>` 标签只有微信支付权限的公众号才能用
5. **内容限制**：content < 2万字符、< 1MB
