## 项目编码规范（冯子格个人项目）

### 命名约定
- 所有变量名称以 `fzg_` 开头
- 所有 CSS 类名以 `fzg_` 开头（如 `.fzg_container`、`.fzg_btn`）
- 所有 HTML id 以 `fzg_` 开头（如 `id="fzg_header"`、`id="fzg_app"`）

### 文件注释
- 每个 HTML 文件顶部必须包含作者注释块：
  ```
  <!--
    姓名：冯子格
    日期：YYYY-MM-DD
    功能：<页面功能描述>
  -->
  ```

### 技术栈约束
- 仅使用原生 HTML、CSS、JavaScript，**不引入任何第三方库或 CDN**
- 图标统一使用项目 `./font/` 目录下的 iconfont 本地图片文件
- 获取服务器端数据统一使用原生 `fetch()` API，不使用 axios/jQuery 等库
- 样式使用原生 CSS（可使用 CSS 变量），不使用预处理器或框架

### 项目结构
```
d:\web\
├── font/           ← 本地 iconfont 图标 PNG
├── img/            ← 图片素材
├── css/            ← 样式文件
└── *.html          ← 页面文件
```
