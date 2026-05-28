# HTML 学习笔记

创建时间：2026-05-24 13:32

编写:DEEPSEEK_API
标签:# HTML 学习笔记

HTML（HyperText Markup Language，超文本标记语言）是构建网页的标准标记语言。它使用一系列标签来描述网页的结构和内容。HTML 不是编程语言，而是一种标记语言，用来定义文档的各个部分该怎么显示或布局。

---

## 一、HTML 基础概念

### 1.1 什么是 HTML？
- **超文本**：指可以包含图片、链接、音频、视频等非文本内容的文本。
- **标记语言**：通过标签（标记）来“告诉”浏览器如何组织和展示内容。

### 1.2 HTML 文档基本结构
一个最简单的 HTML 文档如下：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>页面标题</title>
</head>
<body>
    <h1>欢迎来到我的网站</h1>
    <p>这是一个段落。</p>
</body>
</html>
```

**结构说明：**
- `<!DOCTYPE html>`：声明文档类型，告诉浏览器使用 HTML5 标准。
- `<html>`：根元素，包括整个页面内容。`lang` 属性指定语言。
- `<head>`：包含文档元数据，如字符集、标题、样式、脚本等。
- `<body>`：可见的页面内容。

---

## 二、HTML 元素与标签

### 2.1 元素和标签的区别
- **标签**：由尖括号包围的关键词，如 `<p>`、`</p>`。
- **元素**：由开始标签、内容和结束标签组成，例如 `<p>内容</p>`。
- 有些标签是**自闭合**（空元素），如 `<br>`、`<img>`、`<input>`，没有结束标签。

### 2.2 嵌套与层级
HTML 元素可以嵌套，形成父子关系。必须正确闭合，不能交叉。

```html
<p>这是一个 <strong>加粗</strong> 的文字。</p>
```

### 2.3 属性
属性提供元素的额外信息，写在开始标签内，格式为 `属性名="值"`。

常见属性：
- `class`：定义元素的类名，用于 CSS 或 JavaScript。
- `id`：定义元素的唯一标识。
- `style`：内联样式。
- `src`：指定图片、脚本等资源的路径。
- `href`：指定链接的目标 URL。
- `alt`：图片的替代文本。

示例：
```html
<a href="https://example.com" target="_blank">访问示例网站</a>
<img src="photo.jpg" alt="一张照片" width="200" height="100">
```

---

## 三、常用 HTML 标签

### 3.1 标题标签 `<h1>` ～ `<h6>`
定义六级标题，`<h1>` 最重要，`<h6>` 最次要。

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
```

### 3.2 段落与文本格式化
- `<p>`：段落。
- `<br>`：换行。
- `<strong>` 或 `<b>`：粗体（`<strong>` 有语义强调）。
- `<em>` 或 `<i>`：斜体（`<em>` 有语义强调）。
- `<u>`：下划线，不常用（建议用 CSS）。
- `<s>`：删除线，不常用。
- `<small>`：小号文字。
- `<mark>`：高亮标记。
- `<sub>` / `<sup>`：下标/上标。
- `<blockquote>`：长引用块。
- `<q>`：短引用，自动加引号。
- `<pre>`：预格式化文本，保留空格和换行。
- `<code>`：代码片段。

### 3.3 链接 `<a>`
用于创建超链接。核心属性：`href`（目标地址）。

```html
<a href="https://www.example.com">这是一个链接</a>
<a href="mailto:someone@example.com">发送邮件</a>
<a href="#section1">跳转到页面内锚点</a>
```

- `target="_blank"`：新窗口打开。
- 锚点设置：目标元素添加 `id="section1"`。

### 3.4 图片 `<img>`
嵌入图片。`src` 指定图片路径，`alt` 是替代文本（无障碍重要）。

```html
<img src="logo.png" alt="公司logo" width="100" height="50">
```

图片格式：JPEG、PNG、GIF、SVG、WebP。

### 3.5 列表
- **无序列表** `<ul>` + `<li>`
```html
<ul>
    <li>项目一</li>
    <li>项目二</li>
    <li>项目三</li>
</ul>
```
- **有序列表** `<ol>` + `<li>`
```html
<ol>
    <li>第一步</li>
    <li>第二步</li>
</ol>
```
- **定义列表** `<dl>` + `<dt>` + `<dd>`
```html
<dl>
    <dt>HTML</dt>
    <dd>超文本标记语言</dd>
    <dt>CSS</dt>
    <dd>层叠样式表</dd>
</dl>
```

### 3.6 表格 `<table>`
用于展示表格数据。

```html
<table border="1">
    <caption>员工信息</caption>
    <thead>
        <tr>
            <th>姓名</th>
            <th>部门</th>
            <th>工号</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>张三</td>
            <td>技术部</td>
            <td>001</td>
        </tr>
        <tr>
            <td>李四</td>
            <td>市场部</td>
            <td>002</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">总计：2人</td>
        </tr>
    </tfoot>
</table>
```

- `<thead>`、`<tbody>`、`<tfoot>`：表格语义化分区。
- `colspan`、`rowspan`：跨列、跨行。
- 尽量不使用表格布局，仅用于数据展示。

### 3.7 表单 `<form>`
用于收集用户输入。常用属性 `action`（提交地址）、`method`（GET/POST）。

```html
<form action="/submit" method="POST">
    <label for="username">用户名：</label>
    <input type="text" id="username" name="username" required>

    <label>密码：
        <input type="password" name="password">
    </label>

    <label>性别：</label>
    <input type="radio" name="gender" value="male"> 男
    <input type="radio" name="gender" value="female"> 女

    <label>爱好：</label>
    <input type="checkbox" name="hobby" value="reading"> 阅读
    <input type="checkbox" name="hobby" value="sports"> 运动

    <label for="country">国家：</label>
    <select id="country" name="country">
        <option value="china">中国</option>
        <option value="usa">美国</option>
    </select>

    <label>简介：</label>
    <textarea name="bio" rows="4" cols="30"></textarea>

    <button type="submit">提交</button>
    <button type="reset">重置</button>
</form>
```

**常用 `<input>` 类型：**
- `text`：文本
- `password`：密码
- `email`：电子邮件
- `number`：数字
- `date`：日期
- `file`：文件上传
- `submit`：提交按钮
- `checkbox`：多选
- `radio`：单选
- `hidden`：隐藏字段

### 3.8 分区与容器
- `<div>`：块级无语义容器，用于布局。
- `<span>`：行内无语义容器，用于包裹文本局部。

---

## 四、HTML5 语义化标签

使用具有明确含义的标签，提升可读性和 SEO。

| 语义标签 | 用途 |
|----------|------|
| `<header>` | 页面或区块的头部 |
| `<nav>` | 导航链接区域 |
| `<main>` | 主要内容区域（每个页面一个） |
| `<article>` | 独立的文章内容 |
| `<section>` | 文档中的节（有一定主题） |
| `<aside>` | 侧边栏或附加内容 |
| `<footer>` | 页面或区块的底部 |
| `<figure>` / `<figcaption>` | 插图、图表及其标题 |

```html
<header>
    <h1>我的博客</h1>
    <nav>
        <a href="/">首页</a>
        <a href="/about">关于</a>
    </nav>
</header>
<main>
    <article>
        <h2>文章标题</h2>
        <p>正文…</p>
    </article>
</main>
<footer>
    <p>&copy; 2025 我的博客</p>
</footer>
```

---

## 五、多媒体嵌入

### 5.1 音频 `<audio>`
```html
<audio controls>
    <source src="music.mp3" type="audio/mpeg">
    您的浏览器不支持音频播放。
</audio>
```
- `controls`：显示播放控件。
- `autoplay`：自动播放（浏览器会限制）。
- `loop`：循环播放。

### 5.2 视频 `<video>`
```html
<video width="640" height="360" controls>
    <source src="movie.mp4" type="video/mp4">
    您的浏览器不支持视频播放。
</video>
```

### 5.3 内嵌内容 `<iframe>`
在当前页面嵌入另一个 HTML 页面。常用于地图、广告等。
```html
<iframe src="https://example.com" width="600" height="400"></iframe>
```
注意安全性，可添加 `sandbox` 属性限制行为。

---

## 六、HTML 头部元素

- `<title>`：网页标题（显示在浏览器标签页）。
- `<meta charset="UTF-8">`：字符编码声明。
- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`：移动端视口设置。
- `<meta name="description" content="页面描述">`：SEO 描述。
- `<link rel="stylesheet" href="style.css">`：引入外部 CSS。
- `<style>`：内嵌 CSS。
- `<script src="app.js" defer></script>`：引入外部 JavaScript。
- `<base href="https://example.com/">`：基础 URL，影响相对路径。

---

## 七、HTML 注释与特殊字符

### 7.1 注释
```html
<!-- 这是注释，不会显示在页面上 -->
```

### 7.2 字符实体
因为 `<`、`>` 等有特殊含义，需要用实体显示。

| 字符 | 实体名称 | 实体编号 |
|------|----------|----------|
| <    | `&lt;`   | `&#60;`  |
| >    | `&gt;`   | `&#62;`  |
| &    | `&amp;`  | `&#38;`  |
| "    | `&quot;` | `&#34;`  |
| 空格 | `&nbsp;` | `&#160;` |
| ©    | `&copy;` | `&#169;` |

---

## 八、HTML 实践建议与最佳实践

1. **使用正确的 DOCTYPE**：`<!DOCTYPE html>`。
2. **语义化优先**：用合适的标签，而非全是 `<div>`。
3. **合理嵌套**，保持代码整洁。
4. **图片必须提供 `alt` 属性**，提升无障碍体验。
5. **表单关联标签**：使用 `<label>` 配合 `for` 或包裹输入框。
6. **外部资源位置**：CSS 放在 `<head>`，JavaScript 放在 `</body>` 前（或使用 `defer`/`async`）。
7. **移动端适配**：添加 viewport meta 标签。
8. **验证 HTML**：通过 [W3C 校验器](https://validator.w3.org/) 检查错误。
9. **学习路径**：先掌握内容标签，再结合 CSS 布局，最后学习 JavaScript 交互。

---

## 九、总结

HTML 是前端开发的基石，掌握了 HTML，就能构建网页的基本骨架，承载文本、图片、链接、表单、多媒体等内容。配合 CSS 和 JavaScript，可以实现精美的界面与交互功能。学习时应注重语义化、结构清晰和可访问性，养成良好的编码习惯。