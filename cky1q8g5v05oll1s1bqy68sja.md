---
title: "Twitter Followers Tracker using Next.js, NextAuth and TailwindCSS"
seoTitle: "Twitter Followers Tracker using Next.js, NextAuth and TailwindCSS"
seoDescription: "Steps to build Twitter followers counter using Next.js, NextAuth, SWR, Tailwind CSS with Dark Mode Support."
datePublished: Sun Mar 12 2023 08:05:33 GMT+0000 (Coordinated Universal Time)
cuid: cky1q8g5v05oll1s1bqy68sja
slug: twitter-followers-tracker-using-nextjs-nextauth-and-tailwindcss
canonical: https://javascript.plainenglish.io/build-a-twitter-followers-counter-using-next-js-nextauth-and-tailwind-dc8a99152af5
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1641398099417/92iCgr_ha.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1641398154880/qPgXrSYKe.png
tags: programming-blogs, javascript, web-development, reactjs, nextjs

---

To learn new things, just reading the docs is not enough. We should practically apply it. Likewise, while learning new tech stacks we should apply them by developing simple apps to get a hands-on experience.

So to learn some new tech stacks let build a small application. Here we are going to learn [Next.js](https://nextjs.org/docs/getting-started), [NextAuth](https://next-auth.js.org/getting-started/introduction), [SWR](https://swr.vercel.app/docs/getting-started) and [Tailwind CSS](https://tailwindcss.com/) by developing a Twitter followers counter app.

> We are going to build an app like [TwiterStats](https://twiter-stats.vercel.app/).

## Tech Stack

1. Next.js for building ReactJS Application.
    
2. NextAuth for OAuth implementation with Twitter.
    
3. SWR for fetching data from API.
    
4. Tailwind for UI
    
5. [Twitter Lite](https://github.com/draftbit/twitter-lite) for fetching data from Twitter APIs.
    

## Next.js and Tailwind Setup

We can setup tailwind with next.js using a single command, as shown below:

```javascript
npx create-next-app -e with-tailwindcss twitter-count
```

The above command automatically configures the Tailwind setup based on the official Next.js example.

Once the installation is completed navigate to your project folder using `cd twitter-count` and start the dev server using `yarn dev` command. You can see the below page if you hit `http://localhost:3000` in the browser.

![nextjs.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641041677306/WLI0jtE4Q.png align="left")

## Configure NextAuth.js

### What is NextAuth?

NextAuth is an open-source Authentication package for Next.js. NextAuth simplifies the social auth logins like Twitter, Google, Apple, Github and many more. It also supports email or passwordless login and database integration.

Add `next auth` to your project using the below command

```javascript
yarn add next-auth
```

Next, create a file named `[…nextauth].js` in `pages/api/auth` folder and add the below code

%[https://gist.github.com/Nilanth/89802fca95dee783c1d53b1536e3716f] 

Let's break down the above code

Above NextAuth function handles the dynamic route for all social auth. Here we are going to use Twitter OAuth, so we have added **TwitterProvider** in providers. To perform successful OAuth we require **TWITTER\_ID** and **TWITTER\_SECRET**, Get these from the [Twitter Developer Platform](https://developer.twitter.com/en) with a few simple steps.

Follow the steps in this [link](https://developer.twitter.com/en/docs/twitter-api/getting-started/getting-access-to-the-twitter-api) to get Twitter API access.

After getting the Secrets from the developer portal, Update it in the env and add to the **provider** as above.

Using **callback** set the required data in session after successful OAuth with Twitter. On Successful OAuth, we get many details from Twitter, Here we will customize the data that we require and save it in session.

We should not expose secrets such as `authToken` and `authSecret` to the client-side, so we save them in JWT token objects. Then we can access the user credential on the server-side using the `getToken` helper method.

`secret` a random string used to hash tokens, sign or encrypt cookies and generate cryptographic keys.

## Configure SessionProvider

Warp the **SessionProvier** context at the top-level component to use `useSession` hooks to get session data in child components as below

%[https://gist.github.com/Nilanth/f6a34c48b197c8a8441525984dcd37b4] 

`refetchInterval` is used to fetch the session periodically in the background.

In our app, `_app.js` is the top-level component, so we have wrapped the session provider. Here we have wrapped ThemeProvide context from [next-theme](https://github.com/pacocoursey/next-themes) to enable dark mode support.

## Followers Counter Component

Add the below code in Followers Components

%[https://gist.github.com/Nilanth/b581d66b73147d65e20ab141137c4510] 

### Break Down the Followers Component

#### What is SWR?

[SWR](https://swr.vercel.app/docs/getting-started) is a React Hooks for Data Fetching developed by the Next.js team. It supports real-time data fetching, built-in cache, Auto Revalidation, Prefetching and more.

In the followers component, we have called `/api/twitter/user` API to get basic details of the Twitter user such as name, followers count, profile description and location. We have used SWR to get the data from the API in an interval of time.   As the data we get from NextOAuth is not real-time data. So we use **Twitter Lite** API to get the Twitter user details in real-time.

## Twitter Lite Integration

[Twitter Lite](https://github.com/draftbit/twitter-lite) is a tiny, full-featured, flexible server library for Twitter APIs.

In Next.js you can build APIs also, files inside `api/*` are considered as API endpoints. Which are processed on the server, not on the client-side. Twitter APIs can be accessed from the server-side only, so we have a user API in the `api/` folder to access the show API using the Twitter lite package.

Add the below code `pages/api/twitter/user.js` to access the user details using `/api/twitter/userAPI`.

%[https://gist.github.com/Nilanth/46096b5b173f4eb136d0cca65454c293] 

Add the Followers component in `index.js` file as below.

%[https://gist.github.com/Nilanth/9b1fca7a90ad45e0ccbf3ba6edee23a6] 

Here we use `signIn` and `signOut` the method from `next-auth` to initiate OAuth login. To log in with Twitter we pass Twitter param to the sign-in method as below

```javascript
signIn('twitter');
```

Now just hit the URL in the browser to see the changes like below

![signin](https://cdn.hashnode.com/res/hashnode/image/upload/v1641041767885/XFqy5y00J.png align="left")

On calling the `signIn` method, the app will be redirected to the Twitter OAuth page and clicking the **Authorize App** button on OAuth Page will redirect back to our followers component as below image.

![cover-image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1641041790185/fpIqddGdJ.png align="left")

> We need to configure the OAuth redirect URL in Twitter Developer Portal when registering.

You can customize the UI based on your need, Here I have covered only the integration part and with basic UI using tailwind.

## Deploying in Vercel

You can deploy your Counter App in Vercel within two steps as below:

1. Create a [Vercel](https://vercel.com/signup) Account
    
2. Connect your repository and click deploy.
    

## Links

**GitHub Repo** -&gt; https://github.com/Nilanth/twiter-stats

**Live Demo** -&gt; https://twiter-stats.vercel.app

## Conclusion

We have successfully integrated Twitter with NextAuth and displayed the follower's count using Next and tailwind. We have got hands-on experience with these tech stacks now.

Thank you for reading

Get more updates on [Twitter](https://twitter.com/Nilanth).