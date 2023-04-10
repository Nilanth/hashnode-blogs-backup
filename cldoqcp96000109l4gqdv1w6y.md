---
title: "Multi-threaded React App using useWorker"
seoTitle: "React App with useWorker for multi-threading"
seoDescription: "UseWorker simplifies web worker setup for CPU-intensive tasks in React, allowing multi-threading without blocking the UI"
datePublished: Mon Apr 10 2023 02:24:50 GMT+0000 (Coordinated Universal Time)
cuid: cldoqcp96000109l4gqdv1w6y
slug: multi-threaded-react-app-using-useworker
canonical: https://javascript.plainenglish.io/multi-threaded-react-app-using-useworker-e67a593c9b51
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1675440759436/482eab54-bea8-498e-aff6-2132a3660830.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1675441036786/22db5422-ad39-41f1-a9ce-f784fad9e8c3.jpeg
tags: javascript, web-development, reactjs, nextjs

---

As we all know, Javascript is a single-threaded language. So, if we do any expensive task, It will block UI interaction. And the user needs to wait till it completes to perform any other action, which gives a bad UX experience.

To overcome and perform such tasks, Javascript has a solution called [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers), Which allows performing the expensive task in web browsers without blocking the user interface and makes the UX very smooth.

Let us see what is web workers first.

## Web Workers

Web Worker is a script that runs in the background without affecting the user interface, as it runs in a separate thread instead of the main thread. So it won’t cause any blocking to the user interaction. Web workers are primarily used to perform expensive tasks in a web browser, like sorting large numbers of data, CSV export, image manipulation, etc.

![worker-thread](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p2ikpn8va49460arsuum.png align="left")

Referring to the above image, we can see that an expensive task is performed parallel by a worker without blocking the main thread. When we perform the same in the main thread, it causes UI blocking.

## What about the Concurrent mode in React?

React [concurrent mode](https://beta.reactjs.org/reference/react/startTransition) does not run tasks in parallel. It moves the non-urgent task to transition and perform the urgent task immediately. It uses the same main thread to process it.

As we see in the following image, urgent tasks are processed using context switching. For example, If a table is rendering a large dataset and the user tries to search for something, React switches the task to user search and processes it first as below.

![task-switch](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7nc8978zlpi8gmrcxlnd.png align="left")

When using a worker for the same task, table rendering runs in a separate thread in parallel. Check the following image.

![react-worker](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4tnoy22tqchmq8cuavdp.png align="left")

## useWorker

[useWorker](https://github.com/alewin/useWorker) is a library to uses web worker APIs in a simple configuration with React Hooks. Which supports executing expensive tasks without blocking the UI, support promises instead of event listeners, and other notable feature are

1. Timeout option to kill the worker
    
2. Remote Dependencies
    
3. Transferable
    
4. Worker status
    

> useWorker is a 3KB library

## Why not JavaScript built-in web worker?

When using javascript web worker, we need to add some complex configurations to set up a worker with multiple lines of code. Using useWorker, we can simplify the worker setup. Let’s see the difference between the two in the following code blocks.

## When using JS Web Worker in React App

```javascript
// webworker.js

self.addEventListener("message", function(event) {
  var numbers = [...event.data]
  postMessage(numbers.sort())
});
```

```javascript

//index.js

var webworker = new Worker("./webworker.js");

webworker.postMessage([3,2,1]);

webworker.addEventListener("message", function(event) {
    console.log("Message from worker:", event.data); // [1,2,3]
});
```

## When using useWorker in React App

```javascript
    // index.js
    
    const sortNumbers = numbers => ([...numbers].sort())
    const [sortWorker] = useWorker(sortNumbers);
    
    const result = await sortWorker([1,2,3])
```

As I said earlier, `useWorker()` simplifies the configuration compared to the plain javascript worker.

Let’s integrate with React App and perform high CPU-intensive tasks to see the `useWorker()` in action.

## Quick Start

To add `useWorker()` to a react project, use the following command

`yarn add @koale/useworker`

After installing the package, import the useWorker().

`import { useWorker, WORKER_STATUS } from "@koale/useworker";`

We import useWorker and WORKER\_STATUS from the library. **useWorker()** hooks return workerFn and controller.

1. `workerFn` is the function that allows running a function, with web workers.
    
2. The controller consists of status and kill parameters. status parameter returns the status of the worker and the kill function used to terminate the current running worker.
    

Let’s see the **useWorker()** with an example.

Sorting a large Array using **useWorker()** and the main thread

First, create a SortingArray component and add the following code

```javascript
    //Sorting.js
    
    import React from "react";
    import { useWorker, WORKER_STATUS } from "@koale/useworker";
    import { useToasts } from "react-toast-notifications";
    import bubleSort from "./algorithms/bublesort";
    
    
    const numbers = [...Array(50000)].map(() =>
      Math.floor(Math.random() * 1000000)
    );
    
    function SortingArray() {
      const { addToast } = useToasts();
      const [sortStatus, setSortStatus] = React.useState(false);
      const [sortWorker, { status: sortWorkerStatus }] = useWorker(bubleSort);
      console.log("WORKER:", sortWorkerStatus);
      const onSortClick = () => {
        setSortStatus(true);
        const result = bubleSort(numbers);
        setSortStatus(false);
        addToast("Finished: Sort", { appearance: "success" });
        console.log("Buble Sort", result);
      };
    
      const onWorkerSortClick = () => {
        sortWorker(numbers).then((result) => {
          console.log("Buble Sort useWorker()", result);
          addToast("Finished: Sort using useWorker.", { appearance: "success" });
        });
      };
    
      return (
        <div>
          <section className="App-section">
            <button
              type="button"
              disabled={sortStatus}
              className="App-button"
              onClick={() => onSortClick()}
            >
              {sortStatus ? `Loading...` : `Buble Sort`}
            </button>
            <button
              type="button"
              disabled={sortWorkerStatus === WORKER_STATUS.RUNNING}
              className="App-button"
              onClick={() => onWorkerSortClick()}
            >
              {sortWorkerStatus === WORKER_STATUS.RUNNING
                ? `Loading...`
                : `Buble Sort useWorker()`}
            </button>
          </section>
          <section className="App-section">
            <span style={{ color: "white" }}>
              Open DevTools console to see the results.
            </span>
          </section>
        </div>
      );
    }
    
    export default SortingArray;
```

Here we have configured the useWorker and passed the bubleSort function to perform the expensive sorting using worker.

Next, add the following code to`App.js` component and import the SortingArray component.

```javascript
    //App.js
    
    import React from "react";
    import { ToastProvider } from "react-toast-notifications";
    import SortingArray from "./pages/SortingArray";
    import logo from "./react.png";
    import "./style.css";
    
    let turn = 0;
    
    function infiniteLoop() {
      const lgoo = document.querySelector(".App-logo");
      turn += 8;
      lgoo.style.transform = `rotate(${turn % 360}deg)`;
    }
    
    
    export default function App() {
    
      React.useEffect(() => {
        const loopInterval = setInterval(infiniteLoop, 100);
        return () => clearInterval(loopInterval);
      }, []);
    
      return (
        <ToastProvider>
          <div className="App">
            <h1 className="App-Title">useWorker</h1>
            <header className="App-header">
              <img src={logo} className="App-logo" alt="logo" />
              <ul>
                <li>Sorting Demo</li>
              </ul>
            </header>
            <hr />
          </div>
          <div>
            <SortingArray />
          </div>
        </ToastProvider>
      );
    }
```

We have added the react logo to the **App.js** component, which rotates for every **100ms** to visually represent the blocking and non-blocking UI when performing expensive tasks.

When running the above code, we can see two buttons Normal Sort and Sort using **useWorker()**.

Next, Click the Normal Sort button to sort the array in the main thread. We can see the react logo stops rotating for a few seconds. Due to the UI rendering being blocked by the sorting task, the logo resumes rotating after the sorting is completed. This is due to both tasks being processed in the main thread. Check the following gif

![normal-sorting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k74iuo6qd36qbvpr9iaz.gif align="center")

Let’s check the performance profiling of this using the [chrome performance recording](https://developer.chrome.com/docs/devtools/performance/).

![performance-normal](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8eclh8a6o7g9xzta03ic.png align="left")

We can see the Event: click task has taken **3.86 seconds** to complete the process and it has blocked the main thread for 3.86 seconds.

Next, let’s try the Sort using **useWorker()** option. When clicking it we can see the react logo still rotates without interruption. As the useWorker performs the sorting in the background without blocking the UI. Which makes the UX very smooth. Check the following gif

![worker-sorting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xe5ci0p3hy5nca4321cg.gif align="center")

You can also see the worker status as **RUNNING**, **SUCCESS** in the console using the `sortWorkerStatus`.

Let's see the performance profiling results for this approach

![main-thread](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bxsl696fld6u79dqpwra.png align="left")

![worker-thread](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fcnwe2lczguyxgfqftrj.png align="left")

As we can see, the first image represents that there is no long-running process in the main thread. In the second image, we can see the sorting task is handled by a separate worker thread. So the main thread is free from blocking tasks.

You can play around with the entire example in the following sandbox.

%[https://codesandbox.io/embed/useworker-sorting-example-041qhc?fontsize=14&hidenavigation=1&theme=dark] 

## When to use worker

1. Image Processing
    
2. Sorting or Processing large data sets.
    
3. CSV or Excel export with large data.
    
4. Canvas Drawing
    
5. Any CPU-intensive tasks.
    

## Limitation in useWorker

1. The web worker doesn’t have access to the window object and document.
    
2. While the worker is running we can’t call it again until it’s finished, or until it is killed. To get around this we can create two or more instances of the `useWorker()` hook.
    
3. The web worker cannot return the function because the response is serialized.
    
4. Web Workers are limited by the available CPU core and memory of the end user machine.
    

## Conclusion

Web Worker allows using multi-threading in react apps for performing expensive tasks without blocking the UI. Whereas useWorker allows using the web worker APIs in a simplified hooks approach in react apps. Workers shouldn’t be overused, we should use it only if necessary or it will increase the complexity of managing the workers.

Need to learn more? Feel free to connect on [Twitter](https://twitter.com/Nilanth) :)