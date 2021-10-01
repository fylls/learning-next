![1200px-Nextjs-logo svg](https://user-images.githubusercontent.com/55017307/135534142-d6769604-e601-46b2-939d-0cec6abdae19.png)

## What is NextJS?

NextJS is a react framework that allows us to create pre-rendered react websites whether that be via `server-side rendering` or `static site generation`

`server-side rendering` is when react components are rendered into html pages on the server after a page request come from the browser and `static site generation` is when components are rendered into html pages at build time so that we can just deploy the web pages and javascript bundles to the web and next js allows us to easily do both of these things, meaning that our react components are already rendered into html pages by the time they reach the browser. now from that point onwards the application can behave more like an SPA a single page application

in the all routing can be handled on the client side in the browser now in contrast to this without next react renders components in the browser instead and this is known as client-side rendering

now the benefits of server-side rendering and static site generation are that firstly it can improve a website's performance because components are pre-rendered meaning less work in the browser and secondly it results in better seo than traditional single page applications because the response from the server is a fully rendered html page rather than just a blank one which is what would be returned in a regular react application without next so in the eyes of search engine crawlers it makes our site much more palatable so in this series i'm going to show you how to use next to create a website like this it's a

---

## Installation

the easiest way to get started with next is to use a command called create next app much like create react app for making react applications

```bash
npx create-next-app <name>
```

---

`pages folder` this is where all of our different page components are going to be created the idea being that every page in next has its own components its own react components now at the minute the only page component we have is this index component and this is going to be for the home page and we see we have all of this content

index = homepage
\_app = root

`public folder` this is where all of our public assets like images go

`styles folder` for different css files including css modules

---

## Important Commands

```bash
next dev

next build

next start
```

---

components are pre-rendered before it even reaches the browser during development this is done via server-side rendering so the server renders the component then sends the html file to the browser and that happens on each page request from the browser so if i type in a different url it will look for the component for that url pre-render it and send it to the browser

the job of next is to build static pages and js bundles based on our components and the reason for doing this get static paths property or rather function right here is to first tell next how many html pages need to be made based on our data so next we'll run this function and we'll see this paths property that we return and then it will know how many html pages to create based on this and then for each of those it will run this function and fetch each item that we need and then we put that into the component so it can generate a template for each of these pages and then eventually it will generate an html page for each individual item

---

![vercel-inc-logo-vector](https://user-images.githubusercontent.com/55017307/135534140-4554ea43-1947-4d37-9d4d-eb5c45cd95ba.png)

## Deploying to Vercel

the easiest way to deploy a next application is by using the cell this thing right here which is a hosting platform made by the same people who made next js and it allows us to easily sync our deployment with github so that the cell automatically redeploys our websites whenever we merge a new branch into the main one and this makes itreally easy to update your website andhave it automatically deployed each time you do so so i'm going to show you how to set up

- sign up wth github
- link your repo
- deploy
