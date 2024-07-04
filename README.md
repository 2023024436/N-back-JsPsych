# N-back-JsPsych实验设计（增加页面设计）
# 一、实验设计基本设置教程

## 引言

本教程将向您展示如何使用JsPsych创建一个N-back实验。N-back任务是一种认知任务，要求参与者判断当前呈现的刺激是否与前N个刺激中的一个相同。我们将使用JsPsych库来设置和运行这个实验。

## 准备工作

在开始之前，确保您的电脑已经安装了以下内容：
- 浏览器（推荐使用最新版本的Chrome或Firefox）
- 文本编辑器（如Notepad++、Sublime Text等）

## 下载JsPsych文件

首先，下载JsPsych的核心文件和插件。您可以从JsPsych的官方网站（[JsPsych](https://www.jspsych.org/)）下载最新版本的jspsych.js、jspsych.css和其他插件文件。



## 创建HTML框架

创建一个新的HTML文件，并将以下代码复制粘贴到文件中：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>实验</title>
    <!-- 加载必要的脚本库 -->
    <script src="jspsych.js" type="text/javascript"></script>
    <script src="jspsych-html-keyboard-response.js"></script>
    <!-- 加载所有其他JsPsych插件 -->
    <!-- 在这里添加其他插件的引用 -->
    <link href="jspsych.css" rel="stylesheet" type="text/css" />
    <style>
        /* 在这里添加您的自定义样式 */
    </style>
</head>
<body onload="initExp()">
    <!-- 实验内容 -->
    <div id="display_stage"></div>
</body>
<script lang="javascript">
// 在这里添加JsPsych实验设置的JavaScript代码
</script>
</html>
```


## 初始化实验设置

在 script 标签中的 JavaScript 部分，添加以下代码来初始化实验：
```javascript
function initExp() {
    // JsPsych实验设置和运行代码将在这里添加
}
```

## 设置全屏功能

添加全屏设置功能，允许实验进入全屏模式：
```javascript
var FullScreenOn = {
    type: "fullscreen",
    message: "<p>点击按钮以进入全屏模式...</p>",
    button_label: "全屏",
    fullscreen_mode: true
};

var FullScreenOff = {
    type: "fullscreen",
    fullscreen_mode: false
};
```

## 添加实验说明和准备界面

在实验中，您可以添加说明和准备界面，如：
```javascript
var Show_Instructions = {
    type: "html-button-response",
    stimulus: "<p>在这里添加实验说明。</p>",
    choices: ["继续"]
};
```

## 创建试次和刺激

设置刺激列表和创建试次的功能：
```javascript
var ListOfStimuli = [
    '<p class="stimulus" style="color: red;">A</p>',
    '<p class="stimulus" style="color: blue;">B</p>',
    // 添加更多刺激
];

function createTrials(ntarget, ndistractor) {
    // 创建并返回试次数组
}
```

## 显示刺激任务

使用 html-keyboard-response 插件显示刺激，并根据用户反应记录数据：
```javascript
var ShowStimulus = {
    type: "html-keyboard-response",
    stimulus: function () {
        return ListOfStimuli[currentTrial];
    },
    choices: [" ", "r"],
    trial_duration: 2000, // 修改为您的刺激显示时间
    response_ends_trial: false,
    on_finish: function (data) {
        // 记录和处理数据
    }
};
```

## 运行实验

在 jsPsych.init() 函数中，将所有设置好的组件按照顺序添加到 timeline 中，并在 on_finish 函数中保存数据或进行其他处理：
```javascript
jsPsych.init({
    timeline: [
        FullScreenOn,
        Show_Instructions,
        ShowStimulus,
        // 添加更多实验组件
        FullScreenOff
    ],
    display_element: "display_stage",
    on_finish: function () {
        // 在实验结束时的操作，如保存数据
    }
});
```

# 二、实验设计注意事项

## 实验设计中的JsPsych插件说明

在设计N-back实验时，我们使用了多个JsPsych插件来实现不同的功能。以下是本实验中使用到的JsPsych插件及其用途：

## 使用的JsPsych插件

| 插件名称                      | 主要功能                                          | 用途描述                                                          |
|-------------------------------|--------------------------------------------------|-------------------------------------------------------------------|
| `jspsych-html-keyboard-response` | 显示HTML内容并记录键盘响应                            | 用于显示刺激字母并记录参与者的键盘按键响应                        |
| `jspsych-html-button-response`  | 显示HTML内容并记录按钮响应                            | 用于显示实验指示并记录参与者点击按钮的响应                        |
| `jspsych-audio-button-response` | 播放音频并记录按钮响应                                | 在实验中未使用完整功能，但后续可以用于播放音频刺激并记录响应                   |
| `jspsych-audio-keyboard-response` | 播放音频并记录键盘响应                                | 在实验中未使用完整功能，但后续可以用于播放音频刺激并记录响应                   |
| `jspsych-fullscreen`            | 切换全屏模式                                      | 用于切换实验的全屏模式，保证参与者专注于实验任务                   |
| `jspsych-call-function`         | 调用JavaScript函数                                | 用于执行自定义函数，例如初始化实验参数、生成随机试次等             |

## 插件用途描述

### `jspsych-html-keyboard-response`
- **主要功能**：显示HTML内容并记录键盘响应。
- **在实验中的用途**：用于显示刺激字母并记录参与者按下的键。在N-back任务中，我们使用该插件来呈现每一个字母刺激，并在指定时间内等待参与者的键盘响应。

### `jspsych-html-button-response`
- **主要功能**：显示HTML内容并记录按钮响应。
- **在实验中的用途**：用于显示实验指示并记录参与者点击按钮的响应。该插件在实验的不同阶段（如开始、练习、准备和结束）中显示指示信息，并等待参与者点击按钮以继续进行。

### `jspsych-audio-button-response`
- **主要功能**：播放音频并记录按钮响应。
- **在实验中的用途**：虽然本实验未使用该插件，但它可以用于播放音频刺激并记录参与者的按钮响应。在其他实验设计中，可以用该插件播放声音并记录参与者的反应。

### `jspsych-audio-keyboard-response`
- **主要功能**：播放音频并记录键盘响应。
- **在实验中的用途**：本实验只是用了该插件做实验前的指导语的功能，没有应用到播放音频并且按键的相关功能，可以在之后的更新中设置。

### `jspsych-fullscreen`
- **主要功能**：切换全屏模式。
- **在实验中的用途**：用于切换实验的全屏模式，以确保参与者在实验期间不受外界干扰。进入全屏模式后，参与者会更加专注于实验任务，提高数据的有效性。

### `jspsych-call-function`
- **主要功能**：调用JavaScript函数。
- **在实验中的用途**：用于执行自定义函数，例如初始化实验参数、生成随机试次等。在实验设计中，我们使用该插件来设置实验参数、生成随机刺激序列并调整实验流程。

## 实验设计中的插件使用示例

### 设置全屏模式
```javascript
var FullScreenOn = {
    type: "fullscreen",
    message: "<p>当你按下按钮时，屏幕将进入全屏模式...</p>",
    button_label: "全屏",
    fullscreen_mode: true
};
```


## 该实验所使用的Flexbox属性说明

| 属性名                | 描述                                                            | 可选值                                                     |
|-----------------------|-----------------------------------------------------------------|------------------------------------------------------------|
| `display`             | 定义一个flex容器。                                              | `flex` 或 `inline-flex`                                    |
| `flex-direction`      | 定义主轴方向。                                                  | `row`，`row-reverse`，`column`，`column-reverse`            |
| `justify-content`     | 定义项目在主轴上的对齐方式。                                    | `flex-start`，`flex-end`，`center`，`space-between`，`space-around`，`space-evenly` |
| `align-items`         | 定义项目在交叉轴上的对齐方式。                                  | `flex-start`，`flex-end`，`center`，`baseline`，`stretch`   |
| `align-content`       | 定义多根轴线的对齐方式。                                        | `flex-start`，`flex-end`，`center`，`space-between`，`space-around`，`stretch`      |
| `flex-wrap`           | 定义项目是否换行。                                              | `nowrap`，`wrap`，`wrap-reverse`                           |
| `flex-grow`           | 定义项目的放大比例。                                            | 数值                                                       |
| `flex-shrink`         | 定义项目的缩小比例。                                            | 数值                                                       |
| `flex-basis`          | 定义项目的基准大小。                                            | 长度单位或百分比                                           |
| `align-self`          | 允许单个项目有与其他项目不一样的对齐方式。                       | `auto`，`flex-start`，`flex-end`，`center`，`baseline`，`stretch` |
| `order`               | 定义项目的排列顺序。                                            | 数值                                                       |
| `gap`                 | 定义项目之间的间距。                                            | 长度单位或百分比                                           |
| `row-gap`             | 定义行间距。                                                    | 长度单位或百分比                                           |
| `column-gap`          | 定义列间距。                                                    | 长度单位或百分比                                           |

通过理解和应用该实验设计所运用到的Flexbox属性，您可以试着创建复杂的布局，确保您的实验界面既美观又实用。

## 该实验使用的CSS样式

# 实验使用的CSS样式

| 选择器       | 属性                   | 值                                               | 描述                          |
|--------------|------------------------|--------------------------------------------------|-------------------------------|
| `.stimulus`  | `font-size`            | `50pt`                                           | 设置字体大小                  |
| `.stimulus`  | `font-weight`          | `bold`                                           | 设置字体加粗                  |
| `.stimulus`  | `padding`              | `20px`                                           | 设置内边距                    |
| `.stimulus`  | `border-radius`        | `10px`                                           | 设置边框圆角                  |
| `.stimulus`  | `background-color`     | `#f0f0f0`                                        | 设置背景颜色                  |
| `.stimulus`  | `display`              | `inline-block`                                   | 设置显示为内联块              |
| `.container` | `display`              | `flex`                                           | 设置容器为flex布局            |
| `.container` | `flex-direction`       | `column`                                         | 设置主轴为列方向              |
| `.container` | `height`               | `100vh`                                          | 设置高度为视口高度            |
| `.header`    | `background-color`     | `#4CAF50`                                        | 设置背景颜色                  |
| `.header`    | `color`                | `white`                                          | 设置文本颜色                  |
| `.header`    | `text-align`           | `center`                                         | 设置文本居中                  |
| `.header`    | `padding`              | `10px`                                           | 设置内边距                    |
| `.footer`    | `background-color`     | `#4CAF50`                                        | 设置背景颜色                  |
| `.footer`    | `color`                | `white`                                          | 设置文本颜色                  |
| `.footer`    | `text-align`           | `center`                                         | 设置文本居中                  |
| `.footer`    | `padding`              | `10px`                                           | 设置内边距                    |
| `.content`   | `display`              | `flex`                                           | 设置内容区为flex布局          |
| `.content`   | `flex`                 | `1`                                              | 设置flex属性为1               |
| `.content`   | `flex-direction`       | `row`                                            | 设置主轴为行方向              |
| `.sidebar`   | `background-color`     | `#f4f4f4`                                        | 设置背景颜色                  |
| `.sidebar`   | `width`                | `200px`                                          | 设置宽度                      |
| `.sidebar`   | `padding`              | `10px`                                           | 设置内边距                    |
| `.main`      | `background-color`     | `#fff`                                           | 设置背景颜色                  |
| `.main`      | `flex`                 | `1`                                              | 设置flex属性为1               |
| `.main`      | `padding`              | `10px`                                           | 设置内边距                    |

上述为实验设计所运用到的CSS布局样式，灵活运用这次样式可以帮助你进一步美化你的实验设计页面。
