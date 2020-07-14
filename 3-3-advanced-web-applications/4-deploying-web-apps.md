# Deploying Web Apps

## Objectives
After today's guided project, you should be able to:
* explain how the world wide web works
* explain what it means to "deploy" a static web app
* demonstrate the ability to deploy and maintain a React App using Vercel

## Review: Client / Server
Whenever we're writing React apps, these are web applications that run in a browser, "client-side" or "front-end".

"Server-side" code (Node.js, Python, Ruby, Java, etc) is the "back end" application that works with a SQL database and other resources, providing a specific interface for client apps to be able to interface with those resources.

In the case of a single-page React app (SPA), the server delivers that application code to your browser once. From there on out, your browser does a lot of the heavy lifting and the server is pretty much just there to be a data interface. This is similar for mobile apps, which store application code on your device and consumes an external API in the same way for database interaction and other resources.

As you get more familiar with the big picture of how all of these pieces work together, just be sure to keep in mind which pieces of the architecture run in a browser ("client-side" / "front end") and which run on a server ("server-side" / "back end").

## Static & Dynamic Web Apps
A "static" application has hardcoded data that doesn’t change. While our React apps use data from third-party libraries and provide a user experience that is anything but "static", they still deploy very much like a static app. Your Javascript code is delivered directly to the browser to run client-side.

There's a lot more setup involved in deploying a database-backed web service, but there are also "Platform as a Service" providers like Heroku that help streamline this kind of deployment just like Vercel helps out with deploying React apps. 

## Deployment with Vercel
Vercel (formerly known as ZEIT) is a cloud platform for static sites that allows developers to deploy instantly and host apps with minimal configuration. Their documentation refers to the "JAMstack", which simply means JavaScript, reusable APIs, and prebuilt Markup.

## Helpful Links
* [Vercel](https://vercel.com/)
