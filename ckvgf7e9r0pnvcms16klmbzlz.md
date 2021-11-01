## Don't Optimize Your React App, Use Preact Instead

A few months ago, I wrote an [article based on optimizing react loading time](https://dev.to/nilanth/how-to-reduce-react-app-loading-time-by-70-1kmm) and most of the reader's comments were to try [Preact](https://preactjs.com/) to get default optimization. So I decided to try preact with the same app used for the previous article. Let's first get an intro about Preact.

Preact is a React alternative library with all the react features!.. Preact is a **3KB** library. It is very small compared to react, as react and react-dom gzip size is around **41KB** excluding react-scripts based on [bundlephobia](https://bundlephobia.com/). Some highlighted features of preact are

1. Lightweight Virtual Dom
2. Small in Size
3. Performance optimized by default
4. Integration is simple
5. PWA by default

Now let's see preact in action.

I have developed the same app in React and Preact to test the app performance.


![react](https://cdn.hashnode.com/res/hashnode/image/upload/v1635603144402/8_nY_8ByD.png)

![Preact](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602140053/w45GjCSM1.png)

For react app I used [Create React App](https://create-react-app.dev/) and for Preact used [preact-cli](https://github.com/preactjs/preact-cli). Preact also gives an option to convert your existing react app to preact using [preact-compat](https://github.com/preactjs/preact-compat), but I have built an app from scratch to see the best result.

To compare both app performances, I used [GTmetrix](https://gtmetrix.com/) and hosted both apps in [Netlify](https://www.netlify.com/).

## React App Performance

Below is the score given by **GTMetrics** for React-based App. I have used Route Based **Code Splitting** for the dashboard Component. The performance is **80%** with **B grade**, largest content paint (**LCP**) and Layout Shifting (**CLS**) seems low.

![react-p](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602184408/WkFWmVPwz.png)

As we see in the below image, the entire page is loaded in **2 sec**, First Content Paint is around **1 sec**. Seems the performance is Not bad.

![react-lt](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602237831/NWND-MM60.png)


## Preact App Performance

All the metrics are in Green!!!. Seems the same app in Preact scored **100%** with an **A grade** in GTMetrix. The largest content paint (**LCP**) is less than **500ms**, No Layout Shifting (**CLS**) happened. 


![preact-p](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602276246/pPzugz1Ct.png)

This looks very impressive. Preact optimized our dashboard app quite well. The performance is drastically increased compared to React. Let us check the Loading time

![preact-lt](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602299837/vAnx3b5jH.png)

As we see in the above image. The entire App loads in **1.3 secs** and the Time to First Byte (**TTFB**)is **179ms** !!. Preact seems very faster compared to React and it handles everything by default.

## Comparing both Apps

![preact-pc](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602299837/vAnx3b5jH.png)

![react-pc](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602237831/NWND-MM60.png)


As looking at the page loading side by side, Preact app loads well ahead compared to React and The **Time to interact** is also faster than react app. Preact is [Progressive Web App](https://web.dev/progressive-web-apps/)(PWA) by default so instant loading on repeat visits.


![pwa](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602434973/ljSHtDUPR.png)

Preact also gives some useful warning reg bundle size increase during the build as below

![warning](https://cdn.hashnode.com/res/hashnode/image/upload/v1635602451366/vat8jmhil.png)

## Suspense and Lazy

Some limitation I faced when converting to Preact is that Suspense and lazy loading are experimental and don't support on production as of now. but route based code splitting is enabled by default for the routes directory. 

## Reference

1. [Preact](https://preactjs.com/)
2. [Difference to React](https://preactjs.com/guide/v10/differences-to-react/)

## Conclusion

As based on the above comparison Preact leads in all parts. Due to reduced library size and fast, Preact allows us to focus on developing features instead of manual optimization.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).
