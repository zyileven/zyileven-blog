---
title: '对 JSX 的理解'
description: 'JSX（JavaScript XML）是 React 引入的一种语法扩展，它让你可以在 JavaScript 代码中编写类似 HTML 的代码。这种语法简洁直观，便于描述组件的结构和内容。'
pubDate: '2024-06-04'
heroImage: '/images/2024/6/4/jsx.webp'
---

### JSX 的特点

**HTML-like Syntax（像 HTML）**

在 JavaScript 文件中，JSX 让你可以像编写 HTML 一样编写 UI 结构

```jsx
const element = <h1>Hello, world!</h1>;
```

**表达力强**

JSX 允许你在 UI 代码中嵌入动态内容，通过 `{}` 可以将任何合法的 JavaScript 表达式嵌入到 JSX 中。

```jsx
const name = 'React';
const element = <h1>Hello, {name}!</h1>;
```

**组件结合**

你可以使用 JSX 来创建 React 组件，并将这些组件组合在一起。

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
```

### JSX 与 JavaScript 的关系

JSX 并不是一种独立的语言，而是 JavaScript 的语法扩展。所有的 JSX 代码最终都会被编译成纯 JavaScript。例如，上面的 JSX 代码在编译后会变成如下的 JavaScript 代码：

```jsx
const element = React.createElement('h1', null, 'Hello, world!');
```

而 React 正是实现了这个 createElement 方法来创建一个 React 元素，即虚拟节点。

### 使用 JSX 的注意事项

**必须使用闭合标签**

在 JSX 中，所有的标签必须关闭。即使是单标签元素，也需要使用自闭合形式。

```jsx
const element = <img src="logo.png" alt="Logo" />;
```

**class 变成 className**

因为 `class` 是 JavaScript 的保留字，所以在 JSX 中使用 `className` 来指定 CSS 类。

```jsx
const element = <div className="container"></div>;
```

**CamelCase 驼峰式属性命名**

在 JSX 中，属性名通常使用 CamelCase 命名法，例如 `onClick`、`onChange` 等。

```jsx
const element = <button onClick={handleClick}>Click me</button>;
```

**内联样式**

在 JSX 中，可以使用一个对象来指定内联样式，属性名需要用 CamelCase。

```jsx
const element = <div style={{ backgroundColor: 'red', fontSize: '12px' }}>Hello</div>;
```

### 使用 JSX 的好处

**可读性高**

JSX 让你在同一个文件中编写 HTML 和 JavaScript，这种方式让组件的结构和逻辑紧密结合，提高了代码的可读性和维护性。

**组件化开发**

JSX 非常适合组件化开发。通过 JSX，可以更直观地构建和组合组件。

**社区和工具支持**

由于 JSX 是 React 官方推荐的语法，社区和工具对 JSX 提供了广泛的支持，包括代码高亮、自动补全、代码检查等。



### 总结

JSX 是一种 JavaScript 的语法扩展，让你可以在 JavaScript 中编写类似 HTML 的代码，简化了组件的编写和组合。它通过 `React.createElement` 转换为纯 `JavaScript`，在提高开发效率和代码可读性方面起到了重要作用。







