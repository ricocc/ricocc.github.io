

## Astro 使用 react-fast-marquee 报错 expected a string (for built-in components) 
```bash
▶ src/pages/index.astro
 error   Element type is invalid: expected a string (for built-in components) or a class/function (for composite components) but got: object.
  File:
    D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:4154:11
  Code:
    4153 |       }
    > 4154 |     throw Error(
           |           ^
 but got: " +
      4156 |         ((null == type ? type : typeof type) + ".")
      4157 |     );
  Stacktrace:
Error: Element type is invalid: expected a string (for built-in components) or a class/function (for composite components) but got: object.
    at renderElement (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:4154:11)
    at renderNodeDestructive (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:4375:16)        
    at finishFunctionComponent (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:3715:7)       
    at renderElement (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:3834:9)
    at renderNodeDestructive (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:4375:16)        
    at performWork (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:4987:13)
    at AsyncLocalStorage.run (node:async_hooks:338:14)
    at Immediate._onImmediate (D:\github\ai-web-template\node_modules\react-dom\cjs\react-dom-server.node.production.js:5468:27)       
    at process.processImmediate (node:internal/timers:476:21)
    at process.callbackTrampoline (node:internal/async_hooks:130:17)
```

#### 解决方法： 
+ 1): 在react 组件中添加  `client:only="react` 

```jsx
---
  import MarqueeCard from '@/react/MarqueeCard';
//...
---
  //...
  <MarqueeCard
    client:only="react"
    items={items}
    speed={40}
    direction="left"
    pauseOnHover={false}
    />
```

+ 2):  使用 devnomic-marquee 

- [https://github.com/devnomic/marquee](https://github.com/devnomic/marquee)
- [https://marquee-dev.vercel.app/](https://marquee-dev.vercel.app/)

```bash
npm install @devnomic/marquee
import { Marquee } from "@devnomic/marquee";
import "@devnomic/marquee/dist/index.css";


<Marquee
  fade={true}
  direction="left"
  reverse={false}
  pauseOnHover={false}
  className="" // pass class to change gap or speed
  innerClassName="" // pass class to change gap or speed
>
  <div>Content 1</div>
  <div>Content 2</div>
  <div>Content 3</div>
  <div>Content 4</div>
</Marquee>

```
---
## jiatou 

