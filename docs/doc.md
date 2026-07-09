<p align="center">
  <img src="../images/logo.png" alt="DrewMark Logo">
</p>

# DrewMark JS Editor Documentation

---

## Table of Contents

1. [Project Introduction](#1-project-introduction)
2. [File Structure](#2-file-structure)
3. [Quick Start](#3-quick-start)
4. [UI Interface](#4-ui-interface)
5. [Optional Parameters](#5-optional-parameters)
6. [Multilingual Support](#6-multilingual-support)

---

## 1. Project Introduction

[DrewMark](/drewneon/drewmark) is a full-featured markup language system inspired by [Markdown](https://daringfireball.net/projects/markdown/) and [Showdown](https://github.com/showdownjs/showdown).

DrewMark JS Editor is a WYSIWYG editor tailored specifically for DrewMark. Developed using Vanilla JavaScript, it includes [DrewMark JS Parser](/drewneon/drewmark-js-parser) to enable real-time online editing, previewing, and downloading of both DrewMark source text and parsed results. DrewMark JS Editor supports the complete set of DrewMark syntax rules. Please refer to [DrewMark](/drewneon/drewmark) for detailed syntax specifications.

---

## 2. File Structure

```Javascript
project/
├── js/
│   └── drewmark-editor.min.js // Main program
├── css/
│   └── drewmark-editor.min.css // Stylesheet for DrewMark JS Editor
├── lang/
│   ├── en.json // English source text for translation
│   └── zh-cn.json // Chinese translation of DrewMark JS Editor UI
├── docs
│   ├── doc.md // This document
│   └── doc-cn.md // DrewMark JS Editor documentation (Chinese version)
├── examples
│   ├── sample.html // Complete sampleof DrewMark JS Editor (English UI)
│   ├── demo_content.js // Initial DrewMark content corresponding to the above
│   ├── sample-cn.html // Complete samplemple of DrewMark JS Editor (Chinese UI)
│   ├── demo_content-cn.js // Initial DrewMark content corresponding to the above
│   └── media
│       ├── demo_pic.jpg // Image for DrewMark examples
│       ├── demo_sound.mp3 // Audio for DrewMark examples
│       └── demo_vid.mp4 // Video for DrewMark examples
└── readme.md
```

---

## 3. Quick Start

You can embed DrewMark JS Editor into an HTML page with just a few lines of JavaScript code.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <link rel="stylesheet" href="css/drewmark-editor.min.css"> <!-- Include its Stylesheet -->
</head>
<body>
  <div id="drewmark-editor"></div> <!-- Container element for loading the Editor -->
  <script src="js/drewmark-editor.min.js"></script> <!-- Include DrewMark JS Editor -->
  <script>
    drewmarkEditor(); // Initialize the Editor
  </script>
</body>
</html>
```

---

## 4. UI Interface

### 4.1 Interface Showcase

Landscape Mode:
![Landscape Screenshot](../images/main_ui_h.jpg)

Portrait Mode:
![Portrait Screenshot](../images/main_ui_v.jpg)

### 4.2 Functional Areas

1. Toggle between Edit Area and Preview Area: visible in Portrait Mode only while hidden in Landscape Mode.
2. Toolbar: Click buttons to insert corresponding DrewMark syntax into the Edit Area.
3. Edit Area: Users are able to manually type DrewMark syntax here as well.
4. Preview Area: Displays the parsed result of the Edit Area content in real-time.
5. Status Bar: The left side shows character count statistics of the Edit Area; clicking the button on the right opens the DrewMark Syntax Reference.

### 4.3 Special Key Behaviors

When mannually typing in the Edit Area, certain keyboard keys have special behaviors when the cursor is at specific positions within some syntax structures:

1. Pressing **Enter** at the end of a list item line will automatically continue the same list marker on the next line.
2. Pressing **Enter** at the end of any table row will automatically generate a new table row with the same number of cells as the current row.
3. Pressing **Tab** inside a table cell moves focus to the next cell in the same row and selects its text. If the cursor is already in the last cell of the row, a new cell will be appended to the end of that row.
4. Pressing **Enter** in the middle of text within a table cell inserts `\n` (parsed to `<br>`), hence enabling line breaks within the cell.

---

## 5. Optional Parameters

### 5.1 Shared Parameters

DrewMark JS Editor supports functional adjustments via additional parameters: `drewmarkEditor({opts})`. Multiple parameters should be separated by commas.  rewMark JS Editor relies on the included [DrewMark JS Parser](/drewneon/drewmark-js-parser) to render the Preview Area and controls the parser's behavior through shared parameters. Using the parameters listed below in `drewmarkEditor()` will produce the expected rendering in the Preview Area and trigger corresponding changes in the Toolbar.

| Parameter Name      | Type     | Default Value | Description                                                                                         |
| ------------------- | -------- | ------------- | --------------------------------------------------------------------------------------------------- |
| `enable_emoji`      | boolean  | `false`       | Whether to show the emoji button in the toolbar and parse emoji syntax in the preview               |
| `enable_style`      | boolean  | `false`       | Whether to show the style block button in the toolbar and the style attribute option in the attribute modal box as well as parse style block and style attribute syntax in the preview |
| `enhance_codeblock` | boolean  | `true`        | Whether to append code language display and copy button when parsing code blocks                    |
| `enhance_progress`  | boolean  | `true`        | Whether to append specific numerical values when parsing progress bars                              |
| `disable_syntax`    | array    | `[]`          | Disables specified syntax: corresponding buttons are removed from the toolbar and syntax not parsed |

For detailed descriptions of these parameters above, please refer to the "Optional Parameters" section in [DrewMark JS Parser documentation](/drewneon/drewmark-js-parser/docs/doc.md). Below are parameters exclusive to DrewMark JS Editor.

### 5.2 Single Mode

#### 5.2.1 Enablement

**Parameter Name**: `editor_id`
**Type**: string
**Default Value**: `'drewmark-editor'`
**Usage**:
```Javascript
drewmarkEditor({editor_id: 'target_id'}); // Load the Editor into the container element with `id="target_id"`
```
**Description**: By default, DrewMark JS Editor loads into the container element which `id` attribute is "drewmark-editor". Since the `id` attribute must be unique, there shall be only one DrewMark JS Editor instance on a page, hence Single Mode. Use the `editor_id` parameter to customize the `id` attribute value of the target container element, which must **not** be a tag that does not support child nodes, nor renders its content as-is (such as `<code>` or `<textarea>`). It is recommended to use a `<div>` as the Editor's container element.

---

#### 5.2.2 Initial Content

**Parameter Name**: `init_content`
**Type**: string / array
**Accepted Values**: String / Array / Variable
**Default Value**: `''`
**Usage**:
```Javascript
drewmarkEditor({init_content: 'DrewMark source text'});
```
**Description**: When being loaded by default, both the Edit Area and Preview Area of DrewMark JS Editor are blank. Use this parameter to load the Editor with initial content. Please refer to [sample.html](../examples/sample.html) for an example.

---

#### 5.2.3 Textarea Name

**Parameter Name**: `textarea_name`
**Type**: string
**Default Value**: `content`
**Usage**:
```Javascript
drewmarkEditor({textarea_name: 'desired_name'}); 
```
**Description**: The Edit Area of DrewMark JS Editor is a standard `<textarea>` form element, with `content` as the default value for its `name` attribute. When the Editor is embedded within a form, you can customize its `name` attribute via the `textarea_name` parameter to suit your needs.

---

#### 5.2.4 Textarea Height

**Parameter Name**: `textarea_height`
**Type**: number
**Default Value**: `0`
**Usage**:
```Javascript
drewmarkEditor({textarea_height: 300}); 
```
**Description**: By default, or when using the `editor_id` parameter, there is only one DrewMark JS Editor on the page, and its height attempts to fill the remaining screen space (effectively full-screen). To adjust the Editor's height in this case, provide a numeric value to the `textarea_height` parameter. Note: This height refers to the outer height of the Editor's Edit Area and does not include the toolbar or status bar.

---

#### 5.2.5 Download Feature

**Parameter Name**: `enable_download`
**Type**: boolean
**Default Value**: `false`
**Usage**:
```Javascript
drewmarkEditor({enable_download: true}); 
```
**Description**: By default, users of DrewMark JS Editor are unable to save edited content locally. When the `enable_download: true` parameter is applied, a download button appears at the far right of the toolbar, allowing users to download the content in the Edit Area as a plain-text `.dm` file or a line-by-line `.json` file, or the content of the Preview Area as an `.html` file.

---

#### 5.2.6 Save Callback

**Parameter Name**: `onSave`
**Type**: function
**Usage**:
1. *Scenario A*: REST API Submission + JWT Authentication
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    fetch('/api/post/123', { // Server-side handler URL
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + authToken
      },
      body: JSON.stringify({
        content: text,
        // Additional fields to collect and submit
        category: document.querySelector('#category').value
      })
    });
  }
});
```
2. *Scenario B*: Traditional FormData Submission (PHP receives via $_POST)
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    const fd = new FormData();
    fd.append('content', text);
    // Additional fields to collect and submit
    fd.append('category', document.querySelector('#category').value);
    fetch('/api/save.php', { method: 'POST', body: fd }); // Server-side handler URL
  }
});
```
3. *Scenario C*: Submit Line Array (Server processes each line individually)
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    fetch('/api/save-lines', { // Server-side handler URL
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ lines: lines })
    });
  }
});
```
4. *Scenario D*: Local Draft Storage (No server involvement)
```javascript
drewmarkEditor({
  onSave: ({ text, lines }) => {
    localStorage.setItem('draft', text);
    alert('Draft saved');
  }
});
```

**Description**: This parameter serves as the interface between the Editor and the backend server. When applied, a save button (💾) appears on the right side of the toolbar. Upon clicking the save button, the Editor invokes `onSave` function with an object containing two fields (see table below). It is up to the application developer to decide which fields to submit, what content-Type to use, and whether to include authentication credentials or not.

| Field   | Type       | Description                                                                                                                         |
| ------- | ---------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `text`  | `string`   | The full content of the Edit Area as a string, suitable for direct database storage or file writing.                               |
| `lines` | `string[]` | An array, each element is a line of the Edit Area. Suitable for line-by-line processing (e.g., diffs, line numbering, validation). |

**Server-Side Reception Examples**:

1. he following examples assume the frontend submits in **JSON format** (i.e., `Content-Type: application/json`, `body` is `JSON.stringify(...)`).

+ PHP
```php
// Receive JSON body
 $ data = json_decode(file_get_contents('php://input'), true);
 $ content =  $ data['content'];      // string, corresponds to frontend text
 $ lines   =  $ data['lines'] ?? [];  // array, corresponds to frontend lines (use as needed)
```

+ Python Flask
```python
from flask import request
import json

@app.route('/api/save', methods=['POST'])
def save():
    data = request.get_json()         # Automatically parses application/json
    content = data['content']         # str, corresponds to frontend text
    lines = data.get('lines', [])     # list[str], corresponds to frontend lines
```

+ Python Django
```python
import json
from django.http import JsonResponse

def save(request):
    data = json.loads(request.body)    # Django requires manual JSON parsing
    content = data['content']          # str
    lines = data.get('lines', [])      # list
```

+ Node.js (Express + body-parser)
```js
app.use(express.json());  // Required configuration, otherwise req.body is undefined

app.post('/api/save', (req, res) => {
  const content = req.body.content;  // string
  const lines   = req.body.lines;    // string[]
});
```

2. If **the frontend uses FormData submission** (Scenario B), server reception is identical to standard form submissions:
- PHP: `$_POST['content']` (string)
- Flask: `request.form['content']` (str)
- Django: `request.POST['content']` (str)
- Express (urlencoded): `req.body.content` (string)

---

### 5.3 Multi Mode

#### 5.3.1 Enablement

**Parameter Name**: `editor_class`
**Type**: string
**Default Value**: `''`
**Usage**:
```Javascript
drewmarkEditor({editor_class: 'target_class'}); // Load editors into container elements with `class="target_class"` attribute
```
**Description**: By default, DrewMark JS Editor operates in Single Mode, i.e. only one editor exists on the page. To enable the Multi Mode, i.e. loading multiple editor instances on the same page, please use the `editor_class` parameter. Editors will be initialized in all containers matching the target class name. The container elements for the Editors must not be tags that do **not** support child nodes, nor render their content as-is (such as `<code>` or `<textarea>`). It is recommended to use `<div>` as the Editor's container elements.

---

#### 5.3.2 Multiple Editor Configuration

**Parameter Name**: `multi_editor`
**Type**: array
**Default Value**: `[]`
**Usage**:
```javascript
drewmarkEditor({
  editor_class: 'target_class', // Required parameter to enable the multi mode
  multi_editor: [
    {
      init_content: 'Initial content for the first editor',
      textarea_height: 300,
      textarea_name: 'content_main'
    },
    {
      init_content: ['Multiple line content', 'The second line'],
      textarea_height: 200,
      textarea_name: 'content_side'
    },
    {} // To use all default values
  ]
});
```
**Description**:
1. After enabling the Multi Mode, use the `multi_editor` parameter to configure each editor individually. Each `{}` object corresponds sequentially to one editor instance.
2. Parameters set outside `multi_editor` act as global parameters and are valid for all editors. Identically named parameters set within a specific `multi_editor` entry override the corresponding global parameter for that instance.
3. Once the `multi_editor` parameter is applied, its array length **must** match the number of containers on the page matching the requirement of `editor_class` parameter. Otherwise, no editors will be initialized, and error messages will be displayed in all the targeted containers. For editors requiring no custom configuration, include an empty object (`{}`) as a placeholder. However, this scenario is very rare. It typically requires each `<textarea>` to have a distinct value for the `name` attribute when embedding multiple editors in a form. Although the default naming follows an auto-incrementing pattern (`content_0`, `content_1`, ...), it can hardly meet the actual form requirements.
4. All previously mentioned parameters except `onSave` can be used within `multi_editor`, including parameters shared with DrewMark JS Parser. Among them, the default values of two parameters are different from the Single Mode: `textarea_name` (explained above) and `textarea_height`, which defaults to `200` (px).
5. In the Multi Mode, server submission functionality must be implemented by the form developer. When embedded as form fields within a `<form>`, you can retrieve each editor's content separately via `request.form['textarea_name']`.

---

### 5.4 Parameter Overview

| Parameter Name    | Type           | Default for Single Mode      | Default for Multi Mode                         | Description                                                     |
| ----------------- | -------------- | ---------------------------- | ---------------------------------------------- | --------------------------------------------------------------- |
| `editor_id`       | string         | `drewmark-editor`            | **N/A**                                        | Specify editor's container via `id` attribute                   |
| `editor_class`    | string         | **N/A**                      | `''` (Must be specified)                       | Specify editors' containers via `class` attribute               |
| `init_content`    | string         | `''`                         | `''`                                           | Initial content loaded with the Editor                          |
| `textarea_name`   | string         | `content`                    | `content_0`, `content_1`, ... (auto-increment) | Value of the `name` attribute for the Editor's `<textarea>`     |
| `textarea_height` | number / array | `0` (Fills remaining height) | `200` (px)                                     | Set height of Edit Area and Preview Area                       |
| `enable_download` | boolean        | `false`                      | `false`                                        | Whether to display download button in toolbar                   |
| `onSave`          | function       | `null`                       | **N/A**                                        | Display save button in toolbar for submitting content to server |

---

## 6. Multilingual Support

On load, DrewMark JS Editor reads the `lang` attribute value of the `<html>` tag or `navigator.lanugage` provided by the browser, and searches for a `.json` file named accordingly in the `lang` directory (sibling to `js`). If the language file exists and contains required UI entries, the Editor loads with that language. If no matching file is found or its content is invalid, the built-in English version is used. The project's `lang` directory includes an English source file (`en.json`) for translation purposes.

To modify the default multi-language behavior, use the `drewmarkEditorLang()` function:

**Method I**
1. The `<script>` tag invoking this function must be placed at the end of the HTML body;
2. The `<script>` tag must include the `type="module"` attribute;
3. The function call must be preceded by `await`;
4. This function must be called before `drewmarkEditor()`.

```html
......
    <script type="module">
      await drewmarkEditorLang({opts});
      drewmarkEditor();
    </script>
  </body>
</html>
```

**Method II**
In normal `<script>` tag without `type="module"` attribute, `await` will not work, please use `.then()`.

```javascript
drewmarkEditorLang({opts}).then(function () {
  drewmarkEditor();
});
```

### 6.1 Custom Language File Path

**Parameter Name**: `lang_path`
**Type**: string
**Default Value**: `./lang`
**Accepted Values**: absolute path or relative path
**Usage**:
```javascript
// Method I
await drewmarkEditorLang({lang_path: '/lang_path'});  // use absolute path
// Method II
drewmarkEditorLang({./lang_path}).then(function () { // use relative path
  drewmarkEditor();
});
```
**Description**: By default, DrewMark JS Editor looks for language files in the `lang` directory sibling to its own location. Use this parameter to specify a custom directory for language files.

### 6.2 Custom Fallback Language

**Parameter Name**: `fallback_lang`
**Type**: string
**Default Value**: `en`
**Usage**:
```Javascript
// Method I
await drewmarkEditorLang({fallback_lang: 'language_name'}); 
// Method II
drewmarkEditorLang({fallback_lang: 'language_name'}).then(function () {
  drewmarkEditor();
});
```
**Description**: By default, if the target language file is missing or invalid, DrewMark JS Editor falls back to English. Use this parameter to set a preferred fallback language. However, you **must** ensure that the specified language file exists in the designated language file directory and contains valid content; otherwise, the Editor will still load with the built-in English interface.

---

*Version: v3.8*
