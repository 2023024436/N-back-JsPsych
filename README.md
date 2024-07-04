# N-back-JsPsych实验设计
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
