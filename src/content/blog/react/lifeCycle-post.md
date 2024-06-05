---
title: 'React 中的生命周期'
description: 'useEffect 提供了一种方式来在函数组件中执行副作用（例如，数据获取、订阅或手动更改 DOM）。'
pubDate: '2024-06-05'
heroImage: '/images/2024/6/5/useEffect.png'
---

## 函数式组件开发的生命周期

相比于旧的类组件式开发，函数式组件开发本身不具备生命周期的概念，但是 React 为我们提供了一个名为 useEffect 的自定义 hook，我们可以通过 useEffect 来模拟类组件的各种生命周期。

`useEffect` 提供了一种方式来在函数组件中执行副作用（例如，数据获取、订阅或手动更改 DOM）。



### 模拟componentDidMount

`componentDidMount` 在组件第一次渲染到 DOM 之后调用。要在函数组件中实现类似效果，可以使用一个空依赖数组（`[]`）作为 `useEffect` 的第二个参数。这确保了这个副作用只会在组件挂载时运行一次。

> 注意⚠️，空数组作为依赖项的 useEffect 只会在组件初始化渲染的时候加载一次。

```jsx
import React, { useEffect } from 'react';

function MyComponent() {
    useEffect(() => {
        // 组件挂载时执行的代码
        console.log('Component mounted');

        // 可选的清理函数
        return () => {
            // 组件卸载时执行的代码
            console.log('Component unmounted');
        };
    }, []);

    return <div>My Component</div>;
}

```

### 模拟 componentDidUpdate

`componentDidUpdate` 在组件更新后调用。要在函数组件中实现类似效果，可以在依赖数组中传入希望监听的变量。这会使得 `useEffect` 在依赖变量变化时执行。

```jsx
import React, { useEffect, useState } from 'react';

function MyComponent({ someProp }) {
    useEffect(() => {
        // someProp 改变时执行的代码
        console.log('Component updated with someProp:', someProp);

        // 可选的清理函数
        return () => {
            console.log('Cleanup before someProp changes');
        };
    }, [someProp]);

    return <div>My Component</div>;
}

```

当 someProps 发生变化时，会让 useEffect 执行一次。



### 模拟 componentWillUnmount

`componentWillUnmount` 在组件从 DOM 中移除之前调用。在 `useEffect` 中返回一个清理函数，该函数会在组件卸载时执行。

```jsx
import React, { useEffect } from 'react';

function MyComponent() {
    useEffect(() => {
        return () => {
            // 组件卸载时执行的代码
            console.log('Component unmounted');
        };
    }, []); // 空依赖数组确保只在组件卸载时运行

    return <div>My Component</div>;
}

```

### 在一个 useEffect 中同时实现多个生命周期

```jsx
import React, { useEffect, useState } from 'react';

function MyComponent() {
    const [data, setData] = useState(null);

    useEffect(() => {
        // 组件挂载时获取数据
        fetch('https://api.example.com/data')
            .then(response => response.json())
            .then(data => setData(data));

        // 清理函数，在组件卸载时运行
        return () => {
            console.log('Cleanup on unmount');
        };
    }, []); // 空依赖数组确保只在组件挂载和卸载时运行

    return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
}

```

### 总结

- **`componentDidMount`**: 通过将 `useEffect` 的依赖数组设为空数组（`[]`），确保副作用只在组件挂载时运行一次。
- **`componentDidUpdate`**: 通过在依赖数组中传入需要监听的变量，使副作用在这些变量变化时运行。
- **`componentWillUnmount`**: 通过在 `useEffect` 中返回一个清理函数，该函数会在组件卸载时执行。

通过这些方式，`useEffect` 提供了一个强大且灵活的机制，可以在函数组件中模拟类组件的生命周期方法。























































