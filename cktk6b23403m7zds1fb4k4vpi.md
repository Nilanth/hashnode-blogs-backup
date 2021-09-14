## How to Reduce React App Loading Time By 70%

We build large-scale apps using React. When building these apps, the major issue we face is app performance. When the app grows larger and larger, the performance might deteriorate. Particularly the initial loading time of the app will be affected more. Initial app loading needs to be fast without showing a blank screen for few seconds to the user. As taking more time to load will create a bad impression for the user.

The major cause for this issue is adding too many components into a single bundle file, so the loading of that bundle file might take more time. To avoid this kind of issue, we need to structure our components in an optimized way. To solve this react itself has a native solution, which is code-splitting and lazy loading. Which allows splitting bundle files into a smaller size.

The best place to introduce code splitting is in routes. Route-based code-splitting solve half of the issues. But most of the apps are utilizing only 50% of the advantages of code splitting.

Are we structuring the components properly when using code splitting? We can see why and how to fix it using some code samples. For that, we are going to use a sample React app with some UI components.

In the below screenshot, we can see a dashboard component, which has multiple tabs. Each tab has multiple components.

![dashboard component](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m86yxfplki8f6m4y85ps.png)

The Dashboard component uses route-based code splitting as the below code.

%[https://gist.github.com/Nilanth/afd17cb0cb15b014efb99048f44553b0]

The Dashboard component contains some sub-components like Sales, Profit, Chart, Tiles and Trends like the below code

%[https://gist.github.com/Nilanth/5ed60b31397d81103e1252d71230d396]

We have split the code into routes. so when the app is bundled, we get a separate build file for each route as below

![build-files](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ilf5k7rggx1l1zv2zccb.png)

From the above image, the file with a size 405.1 KB is the dashboard component and other files are for the Header, sidebar, other components and CSS.

I have hosted the app in [Netlify](https://www.netlify.com/) to test the performance. As if we test the app locally we cannot find the difference. When I tested the hosted app with [GTmetrix](https://gtmetrix.com/), the dashboard screen took **2.9 seconds** to load, Check the below image for frame by frame loading.

![frames](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dfgai6a0xk1w7gfbvz10.png)

The dashboard component is the initial page for this app, so when we hit the App URL **405.1KB** file will be loaded along with the header and sidebar.

Initially, the User will view only the **Sales** tab, But our sample app dashboard component has multiple tabs. So the browser is downloading other tabs code also, it is delaying the first paint for the user. To decrease the initial load time, we need to make some changes to the dashboard component as below

%[https://gist.github.com/Nilanth/f4236862a5748873bc9e53fec9689239]

Here I have imported each tab component with lazy loading and wrapped the component with suspense. 


>  Here I have added multiple suspense for better understanding, but you can use single suspense for all the components.

I have not done any changes to route level code-splitting. When we build the app, some extra files are added as we have lazy-loaded each tab in the dashboard component. Check the below image for build file separation.

![build-splitcoding](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/268n08iakvetd2hd0b5k.png)

Now let's test the app with GTmetrix again with the above changes. See the App performance in the below image

![frames-code](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hi2z7p6rtx8gp1h31fox.png)

As you can see, Now our dashboard component is loaded in **1 second**, as **Sales** tab code only loaded now. We have reduced almost **2 seconds** by making some changes. Let see the comparison of route-based and route, component-based code-splitting in the below images.

![route-based-frames](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/refnafbfm38huv20sajl.png)

![component-based-frames](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k2agdjoxwnu2h98543s6.png)

As you see, this is a huge improvement in the app initial load. Now we have reduced the React app initial load time by 70% with a few tweaks by using code splitting effectively in the dashboard component.

## Reference

1. [Code Splitting](https://reactjs.org/docs/code-splitting.html#code-splitting)
2. [First Contentful Paint](https://gtmetrix.com/blog/first-contentful-paint-explained/)

## Conclusion

Structuring components in an optimized way and using React APIs effectively will increase the performance of large-scale apps.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).