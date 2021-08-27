## Build a Portfolio Using Next.js, Tailwind, and Vercel

Steps to build a portfolio website using [Next.js](https://nextjs.org/) and [Tailwind](https://tailwindcss.com/) with Dark Mode Support. 

> **You can build a portfolio like [mine](https://nilanth.vercel.app) after reading this article.** 

A portfolio is a place where you can showcase all your skills to the world. As a developer, you really need a portfolio to showcase your projects, blogs, and much more.

But why do we need to build a portfolio with Next.js? We all know next.js is react framework with out-of-box performance. So you are not required to worry about your portfolio performance. Everything is taken care of by next.js and Vercel. Let's get into action 

## Next.js and Tailwind Configuration

We can configure tailwind with next.js with a single command. As below:

```
npx create-next-app -e with-tailwindcss your-portfolio-name
```

The above command automatically configures your Tailwind setup based on the official Next.js example.

Once the installation is completed navigate to your project folder using `cd your-portfolio-name` and start the dev server using `yarn dev` command. You can see the below page if you hit `http://localhost:3000` in the browser.

![welcome](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sw7fblqfegh7zbck9twq.png)

## Creating Navigation Section

Create a `components` folder in the root directory to add your portfolio components. Create a file called `Navigation.js` and add the below code:

%[https://gist.github.com/Nilanth/4b5585c6983b213acb2d6608d0405a0e]

The navigation component is the header section of your portfolio. In the above code, you can see `dark:` class to support dark mode. Add the `Navigation` component to `_app.js` file as below. MyApp component is used to initialize pages.

%[https://gist.github.com/Nilanth/4bf0c89419feef3a934ba27727e184b0]

## Creating Footer Section

To add a Footer with social links, Create a Footer.js file in the components folder and add the below code:

%[
https://gist.github.com/Nilanth/d0d50cee2cc9eb45e3d99417408f282d
]

Add the `Footer.js` component to `_app.js` file as below

%[
https://gist.github.com/Nilanth/752c63add978a6bcd61074a6a038c593
]

## About Component

Create `About.js` file inside components folder and add the below code:

%[
https://gist.github.com/Nilanth/50bc114a6569a402135a54c544e7a7ec
]

I just added some dummy texts above for the demo. Include your profile image from the public folder as above. Placeholder `blur` prop in image component is to add loading effects. Import `About` component to `index.js` file as below:

%[
https://gist.github.com/Nilanth/53ec8bd2748d4c753166650180b8bbb4
]

I have removed the older template code and added the above code. Now your portfolio looks like below:

![about-screen](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2xvfanljjllcrxfpswm1.png)

## Dark Mode Support

Now let's add dark mode to our portfolio. Adding dark mode is very simple. Create `ThemeSwitch` component to add a toggle switch to toggle between Dark Mode and Light Mode. 

To support Dark Mode in Next.js we need to add `next-themes` package to our dependency. Now import `useTheme` from next-theme to ThemeSwitch Component as below:

%[
https://gist.github.com/Nilanth/c70896816b27f090728169de8cbe3811
]

Add `ThemeSwitch` Component to `Navigation` component and include `next-themes` ThemeProvider in `_app.js` as below:

%[
https://gist.github.com/Nilanth/d71eb49255e46790fa57a08e9df18159
]

`attribute=class` is to enable dark and light mode manually. I have disabled system preference by `enableSystem=false`

Change `darkMode` option to `class` in `tailwind.config.js` file to toggle dark mode manually instead of relying on the operating system preference.

%[
https://gist.github.com/Nilanth/fa5bc67c99dbb2343773828698dbadba
]

After the above changes, our portfolio looks like below:

### Light Mode

![Light Mode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jvcrzfaq5pdkpj5qywbq.png)

### Dark Mode

![Dark Mode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/npd5s823fd85maxpokai.png)

## Deploying in Vercel

You can deploy your portfolio in Vercel within 2 steps as below:
1. Create a [Vercel Account](https://vercel.com/signup)
2. Connect your repository and click deploy.

## Conclusion

You can add multiple pages like projects, blogs by creating new files inside the pages folder. I hope you have found this useful.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).