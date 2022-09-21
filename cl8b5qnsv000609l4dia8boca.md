## Reduce disk space in ReactJS App by 60% using PNPM

Are you working on multiple ReactJS projects with common dependencies? Then this article is for you.

When working on multiple projects or micro frontend apps, you need to install the same dependencies on every project, For instance, If you are working on 5 ReactJS-based projects, all the projects with same dependencies version and each project will have node modules folders, which occupy a large amount of disk space.

We might get a few questions from this.

1. Why is the same dependency installed multiple times without reusing it?
2. How to save disk space when working on multiple projects with the same dependencies?
3. How to speed up the dependencies installation?

In this article, we can see how to resolve this problem using pnpm.

## What is PNPM?

pnpm stands for performant npm. Which is a package manager for NodeJS based projects. which focuses on speed, and an efficient way of handling disk space. It is an alternative to `npm` and `yarn`.

## Highlights

1. Fast
2. Efficient
3. Supports Monorepos

## How PNPM is efficient?

Pnpm handled the disk memory very efficiently. Let's see how

pnpm keeps the dependencies in a global store on your machine, creating a hard link between the projects and dependencies. So the exact dependencies are shared between the projects, saving a lot of space. In npm, it will also duplicate the same dependencies and keep them in the project-specific node modules, which increases the storage space.

## PNPM uses a non-flat directory

By default, pnpm creates a symbolic link between the global store and the project node module. But you can see node modules occupies space in the disk for each project. 

This is due to [hard links](https://unix.stackexchange.com/questions/88423/why-do-hard-links-seem-to-take-the-same-space-as-the-originals), Hard links point to the same place where the original file is located. But only one copy of the dependency is kept in memory for a version. Refer to the below image

![0_ai54jG3TcCGeo9Ph.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1663395005108/M07NC2kSU.jpeg align="left")

## Let’s see a real-time example

**Common Dependencies of each React App**

```
"dependencies": {
"@testing-library/jest-dom": "⁵.16.5",
"@testing-library/react": "¹³.3.0",
"@testing-library/user-event": "¹³.5.0",
"react": "¹⁸.2.0",
"react-dom": "¹⁸.2.0",
"react-scripts": "5.0.1",
"web-vitals": "².1.4"
}
```

### Projects configured using NPM


![Screenshot 2022-09-17 at 10.44.16 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663395027200/KTB0hHtc-.png align="left")

Total Size in Disk: **1260 MB**

### Projects configured using PNPM


![Screenshot 2022-09-17 at 10.44.25 AM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663395038607/J1EN5JW2F.png align="left")


*Note: All the dependencies will be placed in global stores, not individual projects. The above table is for differentiation.*

Total Size in Disk: **500 MB**

Common dependencies are placed in the global store and accessed by the project. As per the above example, common dependencies have **380MB.** As per the above example, we can see we have saved **60% of disk space** using `pnpm` in an efficient way.

## PNPM is faster

pnpm is faster compared to other dependency managers as it doesn’t have blocking stages in installation. Each dependency has its own stage and the next stage starts as soon as possible, by installing each dependency individually.


![0_cKzgS0CyAgWpLUzw.jpeg](https://cdn.hashnode.com/res/hashnode/image/upload/v1663395059592/3lPEY6miK.jpeg align="left")

## Benchmarks

Benchmarks are given by the [pnpm official docs](https://pnpm.io/benchmarks#lots-of-files) using this [package.json](https://github.com/pnpm/pnpm.github.io/blob/main/benchmarks/fixtures/alotta-files/package.json)


![0_8v9hH9IfwIqJ1iUT.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1663395096316/FoHTjfd6y.png align="left")


## Installation

### Using NPM

We can install pnpm globally using npm with the below command

`npm install -g pnpm`

### Using Homebrew

We can install using homebrew with the below command

`brew install pnpm`

## Install as a Standalone Script

### Using Curl


`curl -fsSL https://get.pnpm.io/install.sh | sh -`

### Using wget


`wget -qO- https://get.pnpm.io/install.sh | sh -`


### Create React App using PNPM


We can use the below command to configure a react App

`pnpm create react-app my-pnpm-app`


## Common Commands

`pnpm install` -> install dependencies from package.json

`pnpm add` -> Add dependencies

`pnpm run` -> Run the script in the package.json file

`pnpm test` -> Run tests in the project

`pnpm init` -> Create a package.json file

`pnpm publish` -> Publish a package to the registry

`pnpm start` -> Run a command in package.json to start the app.

## Conclusion

pnpm is faster and handles the disk memory more efficiently than npm and yarn. This gives us lots of free space when working with multiple projects and micro frontend apps. Placing the dependencies on the global store and reusing it is more efficient, which other package manager misses.

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).