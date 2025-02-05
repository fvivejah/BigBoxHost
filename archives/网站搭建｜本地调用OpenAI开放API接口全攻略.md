# 网站搭建｜本地调用OpenAI开放API接口全攻略

## 引言

在探讨如何调用OpenAI开放的API之前，我们首先需要了解几个基本概念：OpenAI、GPT3.5、ChatGPT和API。

### OpenAI概述
**OpenAI** 是一家美国人工智能研究实验室，由非营利组织OpenAI Inc及其营利性子公司OpenAI LP组成。

### ChatGPT简介
**ChatGPT** 是OpenAI开发的人工智能聊天机器人，基于GPT-3.5和GPT-4模型架构，旨在完成会话任务。它不仅是一个聊天应用，也是一种语言模型。

### GPT3.5技术解析
**GPT3.5** 是对GPT-3模型的指令调优和RLHF调优的版本。尽管官方文档显示其参数可能仅为十几亿，但其基于GPT-3的1750亿参数架构。

### API的作用
**API**（应用程序接口）允许不同程序间的数据传输，减少技术人员的重复性工作。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bbtdd.com/WildCard)

## OpenAI开放的API接口简介

## 使用PHP调用OpenAI开放的API

OpenAI官方文档提供了三种API调用方式：cURL、Python和Node.js。本教程将展示如何使用cURL并将其转换为PHP代码来调用API。

### 1. 将cURL转为PHP

推荐使用curl-to-php网站进行转换。

#### 官方API调用代码示例
bash
curl https://api.openai.com/v1/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "text-davinci-003",
    "prompt": "Say this is a test",
    "max_tokens": 7,
    "temperature": 0
  }'


#### 转换后的PHP代码
php
<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, 'https://api.openai.com/v1/completions');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, "{\n    \"model\": \"text-davinci-003\",\n    \"prompt\": \"Say this is a test\",\n    \"max_tokens\": 7,\n    \"temperature\": 0\n  }");

$headers = array();
$headers[] = 'Content-Type: application/json';
$headers[] = 'Authorization: _ENV["Bearer OPENAI_API_KEY"];
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);

$result = curl_exec($ch);
if (curl_errno($ch)) {
    echo 'Error:' . curl_error($ch);
}
curl_close($ch);
?>


### 2. 调整转换后的PHP代码

由于官方API网址在国内可能无法访问，需要对网址进行反代，并添加自己的API Key。

### 3. 配置环境

详细的环境配置步骤包括下载PhpStudy、安装工具、移动文件到WWW文件夹等。

## 美化页面

通过ChatGPT的帮助，我们可以创建更具交互性和美观的界面，例如添加输入框和输出框。

html
<!DOCTYPE html>
<html>
<head>
    <title>MyGPT</title>
    <style>
        /* CSS样式 */
    </style>
</head>
<body>
    <div class="container">
        <h1>MyGPT</h1>
        <form method="POST">
            <label for="input">Input:</label>
            <input type="text" id="input" name="input" placeholder="Enter your message" required>
            <button type="submit">Submit</button>
        </form>
        <div class="output">
            <?php
                // PHP代码处理输入并返回结果
            ?>
        </div>
    </div>
</body>
</html>


## 主要参考文献

通过以上步骤，你可以轻松地在本地环境中调用OpenAI的API，并创建一个功能完善的交互式界面。