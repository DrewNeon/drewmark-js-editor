<p align="center">
  <img src="../images/logo.png" alt="朱码标志">
</p>

# 朱码 JS 编辑器文档

---

## 目录

1. [项目简介](#1-项目简介)
2. [文件结构](#2-文件结构)
3. [快速开始](#3-快速开始)
4. [UI界面](#4-UI界面)
5. [可选参数](#5-可选参数)
6. [多语言支持](#6-多语言支持)

---

## 1. 项目简介

[朱码](../../../../../drewneon/drewmark) 是一款受 [Markdown](https://daringfireball.net/projects/markdown/) 和 [Showdown](https://github.com/showdownjs/showdown) 所启发的全功能型标记语言系统。

*朱码 JS 编辑器*是为朱码量身定制的一款 WYSIWYG 编辑器，基于原生 JavaScript（Vanilla JS）开发，包含 [朱码 JS解析器](../../../../../drewneon/drewmark-js-parser)，从而可实时在线编辑、预览、下载*朱码*原文和解析结果。*朱码 JS 编辑器*支持*朱码*的全部语法规则，请查看[朱码文档](../../../../../drewneon/drewmark/blob/main/docs/doc-cn.md)了解详细的语法规则。

---

## 2. 文件结构

```Javascript
project/
├── js/
│   └── drewmark-editor.min.js // 主程序
├── css/
│   └── drewmark-editor.min.css // 朱码 JS 编辑器的样式文件
├── lang/
│   ├── en.json // 供翻译使用的英文原文
│   └── zh-cn.json // 朱码 JS 编辑器UI界面的中文翻译
├── docs
│   ├── doc.md // 朱码 JS 编辑器文档（英文版）
│   └── doc-cn.md // 本文档
├── examples
│   ├── sample.html // 朱码 JS 编辑器英文界面完整示例
│   ├── demo_content.js // 配合上一项的初始朱码内容
│   ├── sample-cn.html // 朱码 JS 编辑器中文界面完整示例
│   ├── demo_content-cn.js // 配合上一项的初始朱码内容
│   └── media
│       ├── demo_pic.jpg // 配合朱码示例的图片
│       ├── demo_sound.mp3 // 配合朱码示例的音频
│       └── demo_vid.mp4 // 配合朱码示例的视频
└── readme.md 
```

---

## 3. 快速开始

只需几行 Javascript 代码即可将*朱码 JS 编辑器*嵌入 HTML 格式的页面中。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="css/drewmark-editor.min.css"> <!-- 引用编辑器的样式文件 -->
</head>
<body>
  <div id="drewmark-editor"></div> <!-- 加载编辑器的容器标签 -->
  <script src="js/drewmark-editor.min.js"></script> <!-- 引用朱码 JS 编辑器 -->
  <script>
    drewmarkEditor(); // 调用编辑器
  </script>
</body>
</html>
```

---

## 4. UI界面

### 4.1 界面展示

横屏模式：
![横屏截图](../images/main_ui_h-cn.jpg)

竖屏模式：
![竖屏截图](../images/main_ui_v-cn.jpg)

### 4.2 功能区介绍

1. 切换输入框和预览框，仅出现在竖屏模式，横屏模式中隐藏
2. 工具栏：点击按钮向输入框中插入对应的*朱码*语法
3. 输入框：也可以手动书写*朱码*语法
4. 预览框：实时显示输入框中内容的解析结果
5. 状态栏：左侧显示当前输入框中的字符数统计，点击右侧按钮弹出*朱码*语法参考？

### 4.3 特殊按键功能

用户既可以使用工具栏中的各种按钮向输入框中插入各种语法，也可以在输入框中任意输入符合*朱码*语法的文字内容。当光标处于某些语法的特定位置时，某些键盘按键有特殊设定。

1. 在列表语法的行尾处按回车键，将在下一行保持相同的列表语法行首标记。
2. 在表格语法的任意行尾按回车键，将在下一行自动生成与当前行单元格数量相同的表格内容行。
3. 当光标位于表格语法内容行的某个单元格内时按 TAB 键，会跳转到同一行的下一个单元格中并选中其中的文字；如果光标所在的单元格已经是该行最后一个单元格，则会在该行行尾增加一个单元格。
4. 在表格语法内容行的单元格内的文字中间按回车键，将在光标位置插入 `\n` （会被解析器解析输出为 `<br>`），从而实现单元格内换行的效果。

---

## 5. 可选参数

### 5.1 共享参数

*朱码 JS 编辑器*支持通过附加参数来调整功能：`drewmarkEditor({options})`，多个参数之间用逗号分隔。*朱码 JS 编辑器*依赖[朱码 JS 解析器](../../../../../drewneon/drewmark-js-parser)来渲染预览框，并通过共享的参数控制解析器的表现。在 `drewmarkEditor()` 中使用下表中的参数，预览框中将按预期效果呈现，同时工具栏也会发生相应的变化。

| 参数名              | 类型      | 默认值  | 说明                                                                                            |
| ------------------- | -------- | ------- | ---------------------------------------------------------------------------------------------- |
| `enable_emoji`      | boolean  | `false` | 是否在工具栏中显示表情按钮并在预览框中解析表情语法                                                  |
| `enable_style`      | boolean  | `false` | 是否在工具栏中显示样式块按钮以及在添加属性弹出层中是否提供样式属性，并在预览框中解析样式块和样式属性语法 |
| `enhance_codeblock` | boolean  | `true`  | 是否在解析代码块时附加显示代码语言和复制按钮                                                        |
| `enhance_progress`  | boolean  | `true`  | 是否在解析进度条时附加显示具体数值                                                                 |
| `disable_syntax`    | array    | `[]`    | 禁用任意语法，即工具栏中不显示对应的按钮且预览框中不解析相应的语法                                    |

上表中各参数的详细介绍请参见[朱码 JS 解析器文档](../../../../../drewneon/drewmark-js-parser/blob/main/docs/doc-cn.md)的”可选参数”章节。以下是*朱码 JS 编辑器*独有的参数。

### 5.2 单编辑器模式

#### 5.2.1 启用条件

**参数名**：`editor_id`
**类型**：string
**默认值**：`'drewmark-editor'`
**使用方法**：
```Javascript
drewmarkEditor({editor_id: 'target_id'}); // 在 `id="target_id"` 的容器标签中加载编辑器
```
**说明**：默认情况下，*朱码 JS 编辑器*会加载到 `id="drewmark-editor"` 的容器标签中，因为 id 属性具有唯一性，所以页面中只应出现一个*朱码 JS 编辑器*，即单属性模式。使用 `editor_id` 参数可以自定义此 id 名。加载编辑器的容器标签不能是不支持子节点的标签，也不能是直接输出其中内容的标签（例如 `<code>` 或 `<textarea>`），推荐使用 `<div>` 作为编辑器的容器标签。

---

#### 5.2.2 初始内容

**参数名**：`init_content`
**类型**：string / array
**接受值**：字符串 / 数组 / 变量
**默认值**：`''`
**使用方法**：
```Javascript
drewmarkEditor({init_content: '朱码原文'});
```
**说明**：*朱码 JS 编辑器*以默认状态加载时，输入框和预览框中都是空白的，使用此参数可以在编辑器加载时附带初始内容，请参考 [sample-cn.html](../examples/sample-cn.html) 中的用法。

---

#### 5.2.3 文框框名称

**参数名**：`textarea_name`
**类型**：string
**默认值**：`content`
**使用方法**：
```Javascript
drewmarkEditor({textarea_name: 'desired_name'}); 
```
**说明**：*朱码 JS 编辑器*的输入框是一个标准的 `<textarea>` 表单项，其默认 `name` 属性值是 `content`。当编辑器被嵌入到表单中时，可以通过 `textarea_name` 参数自定义其 `name` 属性，从而符合表单的特定需求。

---

#### 5.2.4 文本框高度

**参数名**：`textarea_height`
**类型**：number
**默认值**：`0`
**使用方法**：
```Javascript
drewmarkEditor({textarea_height: 300}); 
```
**说明**：默认情况下或者使用了 `editor_id` 参数时，页面中只存在一个*朱码 JS 编辑器*，其高度会尽量填满屏幕的剩余高度（相当于全屏）；如果此时希望调整编辑器的高度，则须使用一个数值来设置 `textarea_height` 参数。注意：此高度是指编辑器输入框的外部高度，不包含工具栏和状态栏。

---

#### 5.2.5 下载功能

**参数名**：`enable_download`
**类型**：boolean
**默认值**：`false`
**使用方法**：
```Javascript
drewmarkEditor({enable_download: true}); 
```
**说明**：默认情况下，*朱码 JS 编辑器*的工具栏中不提供下载按钮，即用户无法将所编辑的内容下载到本地。当加入 `enable_download: true` 参数之后，工具栏最右侧会出现下载按钮，允许用户将输入框中的内容下载为纯文本格式的 .dm 文件、行数组格式的 .json文件或者将预览框中的内容下载为 .html文件。

---

#### 5.2.6 保存回调

**参数名**：`onSave`
**类型**：function
**使用方法**：
1. *场景 A*：REST API 提交 + JWT 认证
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    fetch('/api/post/123', { // 服务器端处理程序网址
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + authToken
      },
      body: JSON.stringify({
        content: text,
        // 更多需要一并收集并提交的字段
        category: document.querySelector('#category').value
      })
    });
  }
});
```
2. *场景 B*：传统 FormData 表单提交（PHP 用 $_POST 接收）
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    const fd = new FormData();
    fd.append('content', text);
    // 更多需要一并收集并提交的字段
    fd.append('category', document.querySelector('#category').value);
    fetch('/api/save.php', { method: 'POST', body: fd }); // 服务器端处理程序网址
  }
});
```
3. *场景 C*：提交行数组（服务端直接处理每行）
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    fetch('/api/save-lines', { // 服务器端处理程序网址
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ lines: lines })
    });
  }
});
```
4. *场景 D*：本地草稿暂存（不涉及服务器端）
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    localStorage.setItem('draft', text);
    alert('草稿已保存');
  }
});
```

**说明**：此参数是编辑器与服务器后端的交互接口。传入此参数后，工具栏右侧会显示保存按钮（💾）。点击保存按钮时，编辑器调用 `onSave` 并传入一个对象，包含两个字段（详见下表），调用者可自行决定：提交哪些字段、使用何种 Content-Type、是否携带认证信息等。

| 字段    | 类型        | 说明                                                                                |
| ------- | ---------- | ----------------------------------------------------------------------------------- |
| `text`  | `string`   | 编辑器输入框中的完整字符串，适合直接存入数据库字段或写入文件。                            |
| `lines` | `string[]` | 按行拆分的数组，每行都是字符串。适合需要逐行处理的场景（如差异对比、行号标注、逐行校验等）。 |

**服务器端接收示例**：

1. 以下示例假设前端以 **JSON 格式**提交（即 `Content-Type: application/json`，`body` 为 `JSON.stringify(...)`）。

+ PHP
```php
// 接收 JSON  body
$data = json_decode(file_get_contents('php://input'), true);
$content = $data['content'];      // string，对应前端 text
$lines   = $data['lines'] ?? [];  // array，对应前端 lines（按需使用）
```

+ Python Flask
```python
from flask import request
import json

@app.route('/api/save', methods=['POST'])
def save():
    data = request.get_json()         # 自动解析 application/json
    content = data['content']         # str，对应前端 text
    lines = data.get('lines', [])     # list[str]，对应前端 lines
```

+ Python Django
```python
import json
from django.http import JsonResponse

def save(request):
    data = json.loads(request.body)    # Django 需手动解析 JSON
    content = data['content']          # str
    lines = data.get('lines', [])      # list
```

+ Node.js（Express + body-parser）
```js
app.use(express.json());  // 必须配置，否则 req.body 为 undefined

app.post('/api/save', (req, res) => {
  const content = req.body.content;  // string
  const lines   = req.body.lines;    // string[]
});
```

2. 如果**前端使用 FormData 提交**（场景 B），服务端接收方式与普通表单相同：
- PHP：`$_POST['content']`（string）
- Flask：`request.form['content']`（str）
- Django：`request.POST['content']`（str）
- Express（urlencoded）：`req.body.content`（string）

---

### 5.3 多编辑器模式

#### 5.3.1 启用条件

**参数名**：`editor_class`
**类型**：string
**默认值**：`''`
**使用方法**：
```Javascript
drewmarkEditor({editor_class: 'target_class'}); // 在带有 `class="target_class"` 属性的容器标签中加载编辑器
```
**说明**：默认情况下，*朱码 JS 编辑器*为单编辑器模式，即页面中只有一个编辑器。如需启用多编辑器模式，即在同一页面中注入多个编辑器实例，请使用 `editor_class` 参数，编辑器将加载到所有目标类名的容器中。加载编辑器的容器标签不能是不支持子节点的标签，也不能是直接输出其中内容的标签（例如 `<code>` 或 `<textarea>`），推荐使用 `<div>` 作为编辑器的容器标签。

---

#### 5.3.2 多编辑器配置

**参数名**：`multi_editor`
**类型**：array
**默认值**： `[]`
**使用方法**：
```javascript
drewmarkEditor({
  editor_class: 'target_class', // 启用多编辑器的必要参数
  multi_editor: [
    {
      init_content: '第一个编辑器的初始内容',
      textarea_height: 300,
      textarea_name: 'content_main'
    },
    {
      init_content: ['多行内容', '第二行'],
      textarea_height: 200,
      textarea_name: 'content_side'
    },
    {} // 全部使用默认值
  ]
});
```
**说明**：
1. 在启用了多编辑器模式之后，可以通过 `multi_editor` 参数逐一设定每个编辑器的具体参数，每一组 `{}` 按顺序对应一个编辑器实例。
2. 在 `multi_editor` 之外设定的参数作为全局参数对所有编辑器有效，在 `multi_editor` 中针对具体编辑器实例设定的同名参数会覆盖对应的全局参数。
3. 一旦使用了 `multi_editor` 参数，其数组长度**必须**与页面中符合 `editor_class` 参数要求的容器数量一致，否则所有编辑器都无法初始化，全部输出错误提示；对于无需额外设定的编辑器也要为其写一个空白项（`{}`）。不过这种情况鲜有发生，毕竟在表单中嵌入多个编辑器的话，每个 `<textarea>` 都需要赋予 `name` 属性不同的值；默认值虽然是 `content_0`, `content_1`... 这样的自动升序设计，但几乎不可能符合实际表单的需求。
4. `multi_editor` 中可以使用除 `onSave` 之外的所有前述参数，也包括与朱码 JS 解析器共享的参数；其中默认值与单编辑器模式下不同的参数有两个：`textarea_name`（已在上一项中说明）、`textarea_height` 的默认值则是 `200`（px）。
5. 多编辑器模式下向服务器端提交的功能须由表单开发者自行完成。如果将*朱码 JS 编辑器*作为表单项嵌入到 `<form>` 中，则可以通过 `request.form['textarea_name']` 分别获取各编辑器中的朱码内容。

---

### 5.4 参数总览

| 参数名             | 类型           | 单编辑器模式默认值  | 多编辑器模式默认值                        | 说明                                           |
| ----------------- | -------------- | ----------------- | ---------------------------------------- | ----------------------------------------- ---- |
| `editor_id`       | string         | `drewmark-editor` | **无效**                                 | 使用标签的 `id` 属性指定编辑器的加载容器          |
| `editor_class`    | string         | **无效**          | `''` （必须指定）                         | 使用标签的 `class` 属性指定编辑器的加载容器       |
| `init_content`    | string         | `''`              | `''`                                     | 编辑器加载时附带的初始内容                       |
| `textarea_name`   | string         | `content`         | `content_0`, `content_1`, ...（自动升序） | 编辑器中 <textarea> 的 name 属性值              |
| `textarea_height` | number / array | `0`（占满剩余高度） | `200`（px）                              |  指定输入框和预览框的高度                       |
| `enable_download` | boolean        | `false`           | `false`                                  | 是否在工具栏中显示下载按钮                       |
| `onSave`          | function       | `null`            | **无效**                                 | 在工具栏中显示保存按钮用于向服务器端提交*朱码*内容 |

---

## 6. 多语言支持

*朱码 JS 编辑器*在加载时会读取 `<html>` 标签的 `lang` 属性值或者浏览器自带的 `navigator.language`，并默认在与 `js` 平级的 `lang` 目录中寻找以此语言为文件名的 `.json` 文件。如果该语言文件存在且包含界面所需的语言条目，则使用该语言加载编辑器的界面；如果找不到对应文件名的文件或者该文件内容不符合要求，则使用内置的英文版本加载编辑器的界面。本项目的 `lang` 目录中提供了简体中文的语言文件（`zh-cn.json`）以及供翻译用的英文原文（`en.json`）。

如果想对上述多语言的默认状态加以调整，可以使用 `drewmarkEditorLang()` 函数：

**方法一**
1. 使用此函数的 `<script>` 标签须位于 HTML 尾部；
2. `<script>` 标签中须使用 `type="module"` 属性（以便使用 `await`）；
3. 此函数前须使用 `await`；
4. 此函数须写在 `drewmarkEditor()` 函数之前。

```html
......
    <script type="module">
      await drewmarkEditorLang({opts});
      drewmarkEditor();
    </script>
  </body>
</html>
```

**方法二**
使用普通 `<script>` 标签（无 `type="module"` 属性），无法使用 `await`，请用 `.then()` 链式调用：

```javascript
drewmarkEditorLang({opts}).then(function () {
  drewmarkEditor();
});
```

### 6.1 自定义语言文件路径

**参数名**：`lang_path`
**类型**：string
**默认值**：`./lang`
**接受值**：绝对路径或相对路径
**使用方法**：
```javascript
// 方法一
await drewmarkEditorLang({lang_path: '/lang_path'}); // 使用绝对路径
// 方法二
drewmarkEditorLang({lang_path: './lang_path'}).then(function () { // 使用相对路径
  drewmarkEditor();
});
```
**说明**：默认情况下，*朱码 JS 编辑器*会在与其所在目录平级的 `lang` 目录中寻找语言文件，使用此参数可以指定语言文件存储的目录。

### 6.2 自定义保底语言

**参数名**：`fallback_lang`
**类型**：string
**默认值**：`en`
**使用方法**：
```Javascript
// 方法一
await drewmarkEditorLang({fallback_lang: '语言名'}); 
// 方法二
drewmarkEditorLang({fallback_lang: '语言名'}).then(function () {
  drewmarkEditor();
});
```
**说明**：默认情况下，*朱码 JS 编辑器*在找不到目标语言文件或该文件内容不适用时会以英文作为保底语言，使用此参数可以设置希望的保底语言，但**必须**确保该语言文件内容适用且存在于指定的语言文件目录中，否则编辑器仍会以内置的英文版本加载界面。

---

*版本: v3.8*