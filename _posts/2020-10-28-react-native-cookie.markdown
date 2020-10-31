---
title: "React Native的Cookie紀錄"
date: 2020-10-28T18:50:11+08:00
categories: 
  - blog
tag:
  - React Native
---

最近在使用React Native開發跨平台APP使用Fetch時，遇到Server API會記錄的Cookie，導致如果直接使用Fetch會產生非預期的結果。  

例如有一個註冊API如下:
```js
fetch('https://api.example.com/v1/', {
  method: 'POST',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    userName: 'david',
    password: 'password'
  })
});
```
預設會送出cookie導致Server API傳回已經註冊過的問題。

但是可以加上`credentials: 'omit'`後，就可以不會送出Cookie了。

結果改成:
```js
fetch('https://api.example.com/v1/', {
  method: 'POST',
  credentials: 'omit',
  headers: {
    Accept: 'application/json',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    userName: 'david',
    password: 'password'
  })
});
```
沒想到React Native預設會像瀏覽器一樣的行為。  

# 參考在stackoverflow上的問題
> react-native fetch() cookie persist  
> [https://stackoverflow.com/a/41637805](https://stackoverflow.com/a/41637805)  

在2015年11月的React Native 0.16版本，Android及iOS的fetch都會設定`credential`
