# Integrate React Error Boundary with Slack

We might use some third-party services to catch the production errors from React App. Mostly they are paid. Those services provide to integrate with Slack for real-time notification. Production errors need to fix as soon as possible.

To avoid the use of third-party services for slack integration. I have developed a small package to integrate our React App with Slack.

## React Slack Notification

[**React Slack Notification**](https://github.com/Nilanth/react-slack-notification) is a lightweight package, Used to send messages to a Slack channel directly from your react app.

## Let's see how to integrate with our React App.

* Use any one of the below commands to install the package.
    

![npm install command](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/iz1s6mxprrv7hr8z59cf.png align="left")

or

![yarn install command](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jxhxqkcnerwsa5z19sw8.png align="left")

* Follow this [Slack Docs link](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks) to create a WebHook for the channel to which the errors need to send.
    
* Once you get the WebHook from the above step, Add it to your React App `ErrorBoundary` component as below.
    

![React Slack Notification](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gh8lqvvob7b103mfympk.png align="left")

* You can also override the **Channel**, **User Name,** and **Bot icon**, Which you defined when creating the WebHook using the below props.
    

1. `webhook`: Generate using incoming WebHook
    
2. `message`: Text to notify
    
3. `#channel/@username`: Override the channel in WebHook or Direct message to a user in your workspace
    
4. `username`: Message will be displayed using this name
    
5. `botIconURL`: Message bot icon
    

* Once the above configuration is completed, Your React App is now ready to notify the error logs directly to the slack channel without any third-party services.
    

Error logs will be logged in the slack channel, As in the below image.

![Sample Image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c11a4tod4mmdfz664ank.png align="left")

## Conclusion

React Slack Notification solves third-party integration for slack integration.

## Reference

Repo Link: [https://github.com/Nilanth/react-slack-notification](https://github.com/Nilanth/react-slack-notification)

Need to learn more? Feel free to connect on [Twitter](https://twitter.com/Nilanth) :)