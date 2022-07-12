---
title: 给typecho加上友情链接，无需插件
date: 2022-07-12 09:25:00
author: 雨後
img: https://s1.ax1x.com/2022/06/28/jeIj00.jpg
top: false
hide: false
cover: false
toc: false
categories: Typecho
tags:
  - Typecho
---


忘了之前在哪里看到了，回头找到原文地址，再加上

思路是这样的，page页面，按格式填入代码：

```
友情链接的代码如下：
<ul id="flinks">

<li>域名名称</li>

<li>域名地址</li>

<li>域名图标</li>

<li>描述</li>


<li>域名名称</li>

<li>域名地址</li>

<li>域名图标</li>

<li>描述</li>
```

然后页面js会把这些内容隐藏掉，然后通过js去分配每一个支点，然后重新打造新的友情链接的列表

演示看这里：[https://www.dpaoz.com/links.html](https://www.dpaoz.com/links.html)

js代码如下：

```
<script>

(function(){

let a =document.getElementById("flinks");

if(a){

let ns = a.querySelectorAll("li");

let nsl = ns.length;

let str ='<div class="post-lists"><div class="post-lists-body" id ="flinksH">';

let bgid = 0;

const bgs =["bg-blue","bg-purple","bg-green","bg-yellow","bg-red","bg-orange"];

for(let i = 0;i<=nsl-4;i+=4){

           bgid = Math.floor(Math.random() *6);

            str += (`<div class="post-list-item"><div class="post-list-item-container "><div class="item-label ${bgs[bgid]}"><div class="item-title"><a target="_blank" href="${ns[i+1].innerText}">${ns[i].innerText}</a></div><div class="item-meta clearfix"><div class="item-meta-ico bg-ico-book"style="background: url(${ns[i+2].innerText}) no-repeat;background-size: 40px auto;"></div><div class="item-meta-date">${ns[i+3].innerText}</div></div></div></div></div>`);

        }

        str+='</div></div><style></style>';

let n1 = document.createElement("div");

        n1.innerHTML = str;

        a.parentNode.insertBefore(n1,a);

        a.style="display: none;";

    }else{

        console.log('No such id "flinksH"');

    }

}())

</script>
```

css样式代码，放到主题的样式表就可以了

```
.post-lists { position: relative;  display: block;   overflow: hidden;}  

.post-list-item { float: left;  width: 33.3333%; height: auto; padding: 15px;  align-items: center;}

.post-list-item .item-title{font-size: 18px;}

.post-list-item a{ color: #fff; border-bottom: 0px solid #00000070;} 

.post-list-item-container { position: relative; overflow: hidden;  width: 100%; padding: 0; border-radius: 3px;  background-color: #fff; -webkit-box-shadow: 0 1px 4px rgba(0,0,0,.04); box-shadow: 0 1px 4px rgba(0,0,0,.04);}

.post-list-item-container .item-label { position: relative;  height: 130px;    padding: 25px 20px 40px;    background-color: #fff;}

.post-list-item-container .item-label.bg-purple .item-title a { color: #fff;}

.post-list-item-container .item-label .item-meta {  position: absolute; right: 0; bottom: 0;  width: 100%;  padding: 0 15px 15px;  text-align: right;}

.post-list-item-container .item-label .item-meta .item-meta-ico {  display: inline-block;  float: right; width: 42px;  height: 42px; border: 1px solid #eaeaea;  border-radius: 50%;}

.post-list-item-container .item-label.bg-purple .item-meta .item-meta-date { color: #fff;}

.post-list-item-container .item-label .item-meta .item-meta-date { font-size: 12px;  position: relative;   float: left;  padding-left: 5px;   text-align:left;   text-transform: none;  color: #f1f1f1;    max-width: 75%; }

.bg-purple { background-color: #bc99c4!important;}

.bg-yellow { background-color: #f9bb3c!important;}

.bg-orange { background-color: #f68e5f!important;}

.bg-red { background-color: #e8583d!important;}

.bg-green { background-color: #46c47c!important;}

.bg-blue { background-color: #6fa3ef!important;}

.bg-grey { background-color: #f7f7f7!important;}

.bg-deepgrey { background-color: rgba(0,0,0,.5)!important;}

.bg-white { background-color: #fff!important;}
```

具体来说也很简单，可能会有人认为，这样页面就相当于有了2个重复的外链链接，比如14个友情链接，就相当于28个导出链接了（14个是隐藏着），其实js生成的外链对百度来说是无效的，真正意义上页面还是只存在14个友情导出链接，所以就不用担心了

转自：https://www.dpaoz.com/484
