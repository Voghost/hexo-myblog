---
title: vue-element 使用笔记
date: 2021-04-09 17:30:13
tags:
---



## 1. 自定义头部token 
    * 修改 `src/utils/request.js`
```javascript
 if (store.getters.token) {
      // let each request carry token
      // ['X-Token'] is a custom headers key
      // please modify it according to the actual situation
      // config.headers['X-Token'] = getToken()
      config.headers['token'] = getToken()
    }
```

## 2. eslint 报“Expected indentation of 4 spaces but found 6 “错误的解决
```javascript
// rules中添加如下几行
'space-before-function-paren': 0,
'indent': 'off'
```

## 3. 把`request.js` code的20000 修改为200
```

```

## 4. 跨域问题