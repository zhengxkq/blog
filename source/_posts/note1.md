---
title: 纯css实现自适应布局表格
date: {{date}}
categories: 前端
tags: 前端
---
这种布局的特点是使用CSS媒体查询语句(@media screen and (...) )，能根据页面宽度，让页面布局自动做相应的调整，而不是采用传统的做法，几种不同的尺寸就做几个相适应的页面。

```
 body {
        font-family: arial;
    }
    table {
        border: 1px solid #ccc;
        width: 80%;
        margin:0;
        padding:0;
        border-collapse: collapse;
        border-spacing: 0;
        margin: 0 auto;
    }
    table tr {
        border: 1px solid #ddd;
        padding: 5px;
    }
    table th, table td {
        padding: 10px;
        text-align: center;
    }
    table th {
        text-transform: uppercase;
        font-size: 14px;
        letter-spacing: 1px;
    }
    @media screen and (max-width: 600px) {
        table {
            border: 0;
        }
        table thead {
            display: none;
        }
        table tr {
            margin-bottom: 10px;
            display: block;
            border-bottom: 2px solid #ddd;
        }
        table td {
            display: block;
            text-align: right;
            font-size: 13px;
            border-bottom: 1px dotted #ccc;
        }
        table td:last-child {
            border-bottom: 0;
        }
        table td:before {
            content: attr(data-label);
            float: left;
            text-transform: uppercase;
            font-weight: bold;
        }
    }
```


```
<table>
    <thead>
    <tr>
        <th>支付</th>
        <th>日期</th>
        <th>金额</th>
        <th>周期</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td data-label="支付">支付 #1</td>
        <td data-label="日期">02/01/2015</td>
        <td data-label="金额">$2,311</td>
        <td data-label="周期">01/01/2015 - 01/31/2015</td>
    </tr>
    <tr>
        <td data-label="支付">支付 #2</td>
        <td data-label="日期">03/01/2015</td>
        <td data-label="金额">$3,211</td>
        <td data-label="周期">02/01/2015 - 02/28/2015</td>
    </tr>
    </tbody>

```

![pc端效果](https://raw.githubusercontent.com/zhangtingqian/img/master/2.png)
![小于600px的屏效果](https://raw.githubusercontent.com/zhangtingqian/img/master/2-2.png)