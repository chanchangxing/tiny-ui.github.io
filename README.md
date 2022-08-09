# TinyUI 项目网站
[tiny-ui.com](https://tiny-ui.com)

## 协作
网站基于 `GitHub Pages` 和 `Jekyll`，主题是 `just-docs`，如果不需要本地运行网站的话，无需安装相关环境，直接克隆本仓库，创建和编辑 `Markdown` 文件即可，可以参考仓库里已有的 `Markdown` 文件。

> 文章编写规范请遵循：[中文技术文档的写作规范](https://github.com/ruanyf/document-style-guide)

如果想本地运行，预览网站效果的话，可以通过以下命令：
```shell
bundle exec jekyll serve
```

## 目录
**所有文档统一放置在 `docs` 目录中，按照顺序层级进行排列，最终会在网站左边的目录树中展示。**

### 文档顺序
文档头需要增加目录信息说明，`nav_order` 参数代表该文件在左边目录树中的顺序，示例如下：
```markdown
---
layout: default
title: Customization
nav_order: 4
---
```

### 包含子文档（一层）
如果文档有层级关系，
```markdown
+-- ..
|-- (Jekyll files)
|
|-- docs
|   |-- ui-components
|   |   |-- index.md  (parent page)
|   |   |-- buttons.md
|
|-- (Jekyll files)
+-- ..
```

创建父文件夹和 `index.md` 文档，`index.md` 代表父文档，然后设置 `has_children: true` 参数，示例如下：
```markdown
---
layout: default
title: UI Components
nav_order: 2
has_children: true
---

```

子文件里增加 `parent` 参数说明，值为 `parent` 文件里的 `title` 信息，示例如下：
```markdown
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
---
```

### 包含子文档（二层）
如果子文档包含子文档，
```markdown
+-- ..
|
|-- UI Components
|   |-- ..
|   |
|   |-- Buttons
|   |   |-- Button Child Page
|   |
|   |-- ..
|
+-- ..
```
需要设置以下参数：
1. 子文档添加 `has_children` 参数
```markdown
---
layout: default
title: Buttons
parent: UI Components
nav_order: 2
has_children: true
---

```
2. 子子文档添加 `grand_parent` 参数
```markdown
---
layout: default
title: Buttons Child Page
parent: Buttons
grand_parent: UI Components
nav_order: 1
---
```

### 文档结构
建议三层大纲结构：
- 说明
- 示例（截图可选，类似 bottomSheet 最好建议附带截图说明）
- 参数

### 参数说明
1. 参数属性需包含以下字段：
  - 属性名，类型，属性说明，必填，默认值，取值范围
2. 类型统一小写开头，可以写成 string，但是不能写成 String
3. 因为 JavaScript 没有整型，只有 number，如果属性类型只能是整型，建议写成 number（int）
4. function 类型建议增加出入参结构，如 `(res) => void`

### 跳转其他文档
跳转到其他文档，示例如下：
```markdown
[快速开始]({{ site.baseurl }}{% link docs/quick-start.md %})
```

## 资源
**所有资源文件统一放置在 `assets` 目录中，按照文件类型放置，比如图片放在 `assets/images/**.png`。**

## TODO
- [x] 支持中文搜索功能功能 @xiaowzhan
- [x] 左侧大纲结构确认，增加一个调试，@占坤
- [ ] 文档站的版本管理功能
- [ ] 通用 style，attribute 梳理，颜色格式，单位说明  @昶行
- [ ] 自定义组件、API 文档说明，待定，优先级不高

