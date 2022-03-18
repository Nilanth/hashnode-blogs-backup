## Laravel Sanctum Authentication for React App using Breeze

Laravel breeze is an Authentication scaffolding for web and APIs. Breeze is powered by Laravel Sanctum for Authentication system, by default it includes CSRF protections, session authentication and so we don't require to worry about XSS attacks.

In this article, we can see how to use Breeze API scaffolding for authenticating React Applications. Let's integrate

## Laravel Backend Setup

Create a Laravel application and install Laravel breeze API scaffolding using the below commands

```
# Create a laravel application
composer create-project laravel/laravel react-backend

cd react-backend
# Install Breeze

composer require laravel/breeze
php artisan breeze:install api
```

After running the above commands, Update **FRONTEND_URL** in env to **localhost:3000** and serve the application using [Laravel Sail](https://laravel.com/docs/9.x/sail#main-content) or **php artisan serve** command

To test the app, Hit `localhost:8000` in the browser, You can get the app version in response as below.

```
{
  "Laravel": "8.77.1"
}
```

Now the Laravel backend app is ready to handle requests from React app. Next, let's set up the react app

## React App Setup

We will use [Create React App](https://create-react-app.dev/) to set up a React app using the below command

```
npx create-react-app breeze-react

cd breeze-react

yarn start
```

## Configure Axios

To handle APIs, we will use Axios. Add global Axios client as below 

%[https://gist.github.com/Nilanth/acaa459689ccf0b9bd3360d942d1f697]

set `withCredentials` true to enable cross-site cookie access. **REACT_APP_BACKEND_URL** is `localhost:8000` in `.env` file, which is the Laravel backend app created earlier.

## CSRF request

Laravel breeze uses sanctum for authentication, So to authenticate the SPA. we need to make the first request to `/sanctum/csrf-cookie` endpoint. We need to make this request on all non authenticated routes. For instance login, Register, forgot password. 

Create a custom hook in `hooks/auth.js` file and add the below code to handle csrf request

%[https://gist.github.com/Nilanth/204a989d470162044baf572dbf5588bb]

## Integrate Login API

Add the below login function in the `useAuth` hook 

%[https://gist.github.com/Nilanth/1ee06af8e59df77c22ce6d4ed7a4d0ab]

When the login API is requested, first the CSRF API is requested and on success, login API is requested. Likewise, we can use register, forgot password, reset password APIs. Now we have integrated React App with Laravel breeze API scaffolding.

## Laravel Breeze React

[Laravel breeze react](https://github.com/Nilanth/laravel-breeze-react) is the implementation of the Breeze authentication boilerplate for React, available in GitHub. It is preconfigured with all authentication APIs, routes and basic UI using TailwindCSS and CRA.

## Features

1. Prebuild Login, Register, Forgot password, Reset Password and Dashboard UI using [Tailwind CSS](https://tailwindcss.com/)
2. Build with [Create React App 5](https://create-react-app.dev/)
3. [React Router 6](https://reactrouter.com/) for routing
4. [SWR](https://swr.vercel.app/) for revalidation user data
5. [ESLint](https://eslint.org/)

## Quick Start Guide

Clone the **laravel-breeze-react**, install dependencies using `yarn install`, Then, copy the `.env.example` file to `.env` and add the URL of your backend as below

```
REACT_APP_BACKEND_URL=http://localhost:8000
```

Run `yarn start`, Now you will see the below screen in the browser


![home-screen](https://cdn.hashnode.com/res/hashnode/image/upload/v1647589464227/PdU3e-Abz.png)

**laravel-breeze-react** makes you to concentrate only on business logic, as it takes care of the authentication layer.

## Resources

- [Laravel Breeze Docs](https://laravel.com/docs/9.x/starter-kits#breeze-and-next)
- [Laravel Breeze React repository](https://github.com/Nilanth/laravel-breeze-react)
- [Sanctum Docs](https://laravel.com/docs/9.x/sanctum)

## Conclusion

Laravel Breeze makes the SPA Authentication very simple, secure and Laravel Breeze React makes the integration between Laravel Breeze Backend app with React App quickly.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).

## Free eBook

[ReactJS Optimization Techniques and Development Resources](https://nilanth.gumroad.com/l/NYkdN)