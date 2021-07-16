## How to Secure JWT in a Single-Page Application

In this article, we will see how to securely store the JWT token in a single page app for authentication.

## What are all the options we have to store the token in the browser?

1. Local storage
2. Memory
3. Cookie

## JWT in Local Storage
Is local storage is secure to store a token? Let see now, Local storage is accessible from the client-side only, so your API provider will set the JWT in the API response Authorization header as a bearer token in login or Register API if the status success. In React, we will get the JWT and store it in the local storage as below


![image_1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201583916/BySZXl1Q-.png)


![image_2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201607785/o-kO4i1HJ.png)

And for the subsequent request made from the react app, the JWT is taken from local storage and set in the API request Authorization header to maintain the user session


![image_3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201616626/-6pHlUeoE.png)

Values in local storage are accessible by javascript, so any cross-site script can get the JWT from local storage and gain your account access.


![image_4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201625400/nMy_EhpMS.png)

So we should **not use local storage for storing** JWT if you are using, Please update your authentication architecture as local storage is not secure to store a token. Next, let's move to memory

## JWT in Memory (React State)
React state variables will be assigned to default values when the app is refreshed or opened in a new tab, so if the default values are null, when the app is refreshed or opened in a new tab it will be set to null, so when we set the JWT in state variable it will disappear, so the user need to log in each time the app is refreshed or opened in a new tab or the app is closed, it will be poor User Experience. So we cannot store the JWT in the state variable.

Before moving to **JWT in cookie**, Let’s see about what is a cookie and its major attributes

##  Cookie
A cookie is another storage option available in a browser that has an expiration time also, cookie also has some useful attributes to secure it from cross-site scripting (XSS) attacks. Let see what are they in detail

## HttpOnly
A cookie with the HttpOnly attribute is not accessible by Javascript, so we cannot get the cookie as below

``` 
let cookie = document.cookie; 
```

**HttpOnly** cookie can be set and accessed only by the server-side script. This attribute helps to prevent cross-site scripting(XSS) attacks if it’s set with **SameSite=strict**.

## Secure
A cookie with **Secure** attribute will be sent to the server only over the HTTPS request, not in an HTTP request. The **Secure** cookie is encrypted in request and response, so **[Man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack)** attack is prevented by using Secure attribute with **HttpOnly** and **SameSite=strict**.

## SameSite
A cookie with **SameSite=strict** mentions that the cookie is available only for the same site origin requests not for cross-site requests. Now let see how to use the cookie to store JWT.

## JWT in Cookie
A cookie can be set from the server-side and also in the client-side, First we can see how to set and get the JWT from the cookie in the React and using the browser console.

The server set the JWT as a Bearer token in the Authorization response header, In the client-side, the script has access to the token present in the header, we get the token from the response header and set it in the cookie as below


![image_5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201653012/obo0gzlkY.png)


![image_6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201662218/I9lcm_i7i.png)

The cookie is set to the current domain by default and the expiry date is set to 1st Jan 2021. The expiry date is based on the token validity so the token will be removed from the browser cookie once the expiry date reaches.


![image_7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201672163/EBazPMiSL.png)

The cookie needs to send as a bearer token in the API request header on every request made from the client. So, for that, we can get it from the cookie using **document.cookie** property as below


![image_8.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201679706/RD0LxcIUd.png)

document.cookie will return all cookies present against the domain, so we can use  [react-cookie](https://github.com/reactivestack/cookies/tree/master/packages/react-cookie)  package to get a specific cookie as below

![image_9.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201736323/WwLy9vpn3.png)

As we can see that the token is set and get using the script, so we could conclude that handling JWT in the react will lead to XSS (Cross-Site Scripting) attacks same as we saw before while using local storage, but we saw two attributes earlier **HttpOnly** and **Secure**, by setting these attributes will avoid these attacks. But javascript has no access to **HttpOnly** attribute, Only server-side script can access **HttpOnly** attributes. Let see how we can set the JWT from Server Side.

> As previous examples, we saw that JWT is set as Bearer token in authorization header, But handling cookie in server-side we need set the cookie in **Set-Cookie** header and not required to mention the token type as **Bearer**, we can set the JWT directly in **Set-Cookie**.

Here I am using [Express.js](https://expressjs.com) to set JWT in the cookie from the server and we have set **secure** and **HttpOnly** as **true** to restrict the javascript access of JWT in the cookie as below


![image_10.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201767558/mmy3KhwL5.png)

The token in API response **Set-Cookie** header will be saved to browser cookies like in the below image

![image_11.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201775244/hjnVvFaA6.png)

![image_12.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201802381/mi0YCETcW.png)

JWT stored in the cookie will be appended in every API request header automatically as below images

![image_13.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201843110/EhyEAmcZe.png)

![image_14.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610201851434/fqtg_d22v.png)

> But remember that this approach only works if the React app and the BackEnd server hosted in **same domain.**

## Conclusion

Now your app is secured from Cross-Site Scripting (XSS) attacks. I hope you have found this useful. Thank you for reading.

Need to learn more? Feel free to connect on [Twitter](https://twitter.com/Nilanth) :)