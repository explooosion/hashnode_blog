---
title: "React.js - 離開 vue 的我，和從前的 react 夥伴往 useState Lazy Initialization 邁進"
seoTitle: "React.js - 離開 vue 的我，和從前的 react 夥伴往 useState Lazy Initialization 邁進"
seoDescription: "在有需求時發現的新知識，總是特別難忘！"
datePublished: Tue Feb 04 2025 00:00:00 GMT+0000 (Coordinated Universal Time)
cuid: cm6qnhibe000t09l18wun4x8u
slug: reactjs-vue-react-usestate-lazy-initialization
cover: https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2025-02-04_React.js%20-%20%E9%9B%A2%E9%96%8B%20vue%20%E7%9A%84%E6%88%91%EF%BC%8C%E5%92%8C%E5%BE%9E%E5%89%8D%E7%9A%84%20react%20%E5%A4%A5%E4%BC%B4%E5%BE%80%20useState%20Lazy%20Initialization%20%E9%82%81%E9%80%B2/banner/1738683611.png.png
tags: hooks

---

在有需求時發現的新知識，總是特別難忘！

在 react 專案效能調整上，發現了最基礎的玩意。

[![1738683611.png.png](https://raw.githubusercontent.com/explooosion/blogs/refs/heads/main/docs/images/2025-02-04_React.js%20-%20%E9%9B%A2%E9%96%8B%20vue%20%E7%9A%84%E6%88%91%EF%BC%8C%E5%92%8C%E5%BE%9E%E5%89%8D%E7%9A%84%20react%20%E5%A4%A5%E4%BC%B4%E5%BE%80%20useState%20Lazy%20Initialization%20%E9%82%81%E9%80%B2/1738683611.png.png)](https://dotblogsfile.blob.core.windows.net/user/robby/7fac3f0f-753e-4a36-a85e-53a74599e651/1738683611.png.png)

前言
--

因爲工作使用 React 開發，對於許久沒碰的我來說，難免錯過了許多好料。

這篇的原由是有一次「**質疑**」現有專案的寫法：

```javascript
const [list, setList] = useState(() => getList());
```

###### 閱讀他人的代碼，先質疑，再理解。這也是一種成長的方式。

仔細查了，才發現原來這叫做「**useState Lazy Initialization**」。

回到最基礎的文件上，可以找到這篇：[Avoiding recreating the initial state](https://react.dev/reference/react/useState#avoiding-recreating-the-initial-state) 。

它就是在講述使用`useState`，傳入`function`可以使狀態僅在初始時 render。

如果 `function`需要花費較高的運算時間，甚至引起畫面卡頓，那麼這是一個有效提升效能的做法。

###### 中文應該叫做：惰性初始 **state**。

這篇記錄學習內容，閱讀後你應該會知道 useState lazy initialization：

1.  如何正確起手式。
2.  概念與實踐方式。
3.  有無使用的差異。  
     

一、初始化方式的兩種模式
------------

### 1\. 直接傳遞初始值

```javascript
const [todos, setTodos] = useState(createInitialTodos());
```

*   初始值會在 **組件每次渲染時** 計算。
*   如果`createInitialTodos()`運算較重，將會影響效能。

### 2\. 傳遞函數進行 lazy initialization

```javascript
const [todos, setTodos] = useState(() => createInitialTodos());
// or 
const [todos, setTodos] = useState(createInitialTodos);
```

*   React 只會在第一次渲染時執行該函數，並將結果作為初始狀態。
*   避免在每次渲染時執行昂貴的計算。

### 3\. 建立昂貴計算

嘗試將`createInitialTodos`弄得複雜一點，你會發現開始延遲了。

```javascript
/**
 * @param {number} depth
 * @param {number} size
 */
function createInitialTodos(depth = 3, size = 100) {
  if (depth === 0) {
    return Array(size)
      .fill(0)
      .map((_, i) => i);
  }
  return Array(size)
    .fill(0)
    .map(() => createInitialTodos(depth - 1, size));
}
```

二、使用範例來比較效能
-----------

完整範例放在：[https://github.com/explooosion/react-lazy-initialization](https://github.com/explooosion/react-lazy-initialization)

### 1\. 初始 CRA 專案

使用一個乾淨的專案來測試。

```powershell
npx create-react-app my-app
```

\[ App.css \]

記得先移除所有樣式。

### 2\. 建立兩種 Components 比較

沿用剛剛昂貴計算的`function createInitialTodos()`。

建立一個直接傳遞初始值的 Component`AppWithDirectValue`。

\[ App.js \]

```javascript
function AppWithDirectValue() {
  const [count, setCount] = useState(0);

  console.time("Direct initializer");
  const [todos, setTodos] = useState(createInitialTodos());
  console.timeEnd("Direct initializer");

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        AppWithDirectValue ({count})
      </button>
    </div>
  );
}
```

*   在`useState`上下使用`console.time`, `console.timeEnd`記錄時間。
*   在`useState`直接傳入值`createInitialTodos`。
*   使用一個`button`來觸發`re-render`。

以及建立一個傳遞函數進行 lazy initialization 的 Component `AppWithLazyInitializer`。

\[ App.js \]

```javascript
function AppWithLazyInitializer() {
  const [count, setCount] = useState(0);

  console.time("Lazy initializer");
  const [todos, setTodos] = useState(createInitialTodos);
  console.timeEnd("Lazy initializer");

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        AppWithLazyInitializer ({count})
      </button>
    </div>
  );
}
```

*   同樣在`useState`上下使用`console.time`, `console.timeEnd`記錄時間。
*   在`useState`傳入函數`createInitialTodos`，你也可以傳入`() => createInitialTodos()`。
*   使用一個`button`來觸發`re-render`。

接著在 `App` 使用，就可以來比較囉！

\[ App.js \]

```javascript
export default function App() {
  return (
    <>
      <AppWithDirectValue />
      <AppWithLazyInitializer />
    </>
  );
}
```

完整代碼：

\[ App.js \]

```javascript
// @ts-check

import React, { useState } from "react";

/**
 * @param {number} depth
 * @param {number} size
 */
function createInitialTodos(depth = 3, size = 100) {
  if (depth === 0) {
    return Array(size)
      .fill(0)
      .map((_, i) => i);
  }
  return Array(size)
    .fill(0)
    .map(() => createInitialTodos(depth - 1, size));
}

function AppWithDirectValue() {
  const [count, setCount] = useState(0);

  console.time("Direct initializer");
  const [todos, setTodos] = useState(createInitialTodos());
  console.timeEnd("Direct initializer");

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        AppWithDirectValue ({count})
      </button>
    </div>
  );
}

function AppWithLazyInitializer() {
  const [count, setCount] = useState(0);

  console.time("Lazy initializer");
  const [todos, setTodos] = useState(createInitialTodos);
  console.timeEnd("Lazy initializer");

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>
        AppWithLazyInitializer ({count})
      </button>
    </div>
  );
}

export default function App() {
  return (
    <>
      <AppWithDirectValue />
      <AppWithLazyInitializer />
    </>
  );
}
```

三、**Lazy Initialization 合適的場景**
-------------------------------

✅ 適用於初始值計算量大，例如：

*   具有龐大的值或深度的資料。
*   複雜計算，例如來源是解析 JSON、深拷貝物件。
*   只需要在 第一次渲染 設定狀態的情境。  
     

❌ 不適用於：

*   簡單的靜態值，如 `useState(0)`、`useState(false)`。
*   不影響效能的初始化（過度使用 Lazy Initialization 反而讓代碼變得難讀）。

**Reference**
-------------

*   [react dev useState - avoiding-recreating-the-initial-state](https://react.dev/reference/react/useState#avoiding-recreating-the-initial-state)
*   [React Hooks 總整理筆記](https://gcdeng.com/blog/react-hooks#%E6%83%B0%E6%80%A7%E5%88%9D%E5%A7%8B-state)
*   [useState lazy initialization and function updates](https://kentcdodds.com/blog/use-state-lazy-initialization-and-function-updates)  
     

有勘誤之處，不吝指教。ob'\_'ov