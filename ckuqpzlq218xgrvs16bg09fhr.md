## How to Structure Your React Redux App

React is the most popular Javascript library for building user interfaces. React does not have any standard folder structure to group the components and logic. React App can be structured in any way based on the project needs. 

But the improper structuring of the React App will lead to affect the app scalability and maintainability. As the App grows, We might add new and remove some old features, so each component needs to be loosely coupled with each other. Let see how to structure the React app to avoid such issues.

We need to group files based on the feature. That is, All files of a feature are in the same folder. Please check the below image for folder structure

![folder](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138309231/juQ4ipHgw.png)

In the above image we can see the folders of the react app, let's break down each folder purpose.

## app

Global app setup and configuration used by the entire app are defined in app folder as below, which includes axiosClient, rootReducer, saga and store.

![app](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138344259/iDyjKjhDb.png)

## common

Reusable helpers, shared components, hooks, etc are defined in common folder.

![common](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138364220/ljhL5LqRz.png)

## features

Feature specific components, [Slice](https://redux-toolkit.js.org/tutorials/quick-start#create-a-redux-state-slice) (Redux reducer logic and associated actions - [Redux Toolkit](https://redux-toolkit.js.org/)), APIs and styles are placed in the features folder.

![features](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138387753/Qd3oClvTN.png)

## routes

Components private, public routes are defined in routes folders. Route restriction based on authentication is handled here.

![routes](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138408334/u0Yb1bE3G.png)

## assets

Static assets like Images, files, icons are placed in the assets directory.

![assets](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138433662/2qfseIH3E.png)

## tests

Unit test cases and their mock goes to the tests directory. 

![assets](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138454245/RpGVw9etn.png)

## style

Global styles, theme configuration is placed in the style folder.

![style](https://cdn.hashnode.com/res/hashnode/image/upload/v1634138480453/yKMuT-271.png)

Using the above feature folder structure, We can easily remove or add a feature related code without issues. The feature folder structure is recommended by the [redux style guide](https://redux.js.org/style-guide/style-guide#structure-files-as-feature-folders-with-single-file-logic). By using Redux Toolkit, We have avoided boilerplate code like actions and reducers.

> Need to know more about Redux ToolKit. Check out [my article related to the redux toolkit](https://nilanth.hashnode.dev/redux-toolkit-the-standard-way-to-write-redux).

## Resources

1. [Ducks Proposal](https://github.com/erikras/ducks-modular-redux)
2. [File Structuring](https://reactjs.org/docs/faq-structure.html)
3. [Redux Toolkit](https://nilanth.hashnode.dev/redux-toolkit-the-standard-way-to-write-redux)

## Conclusion

Feature folder based file structuring will make react app more maintainable, scalable and loosely coupled.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).