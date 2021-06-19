---
title: "SPA vs SSR vs SSG"
date: 2021-06-17T20:43:12+10:00
draft: false
categories: ["javascript", "React", "Angular", "Vue.js"]
---

CSR (Client Side Rendering), SSR (Server Sided Rendering) and SSG (Static Site Generators) are rendering methods that a developer should be aware of. Today, we will go through the differences, advantages and disadvantages of these rendering approaches.

# Client Side Rendering
In CSR, the client (browser) is responsible for rendering the view. SPAs (Single Page Applications) uses this approach which involves the web server sending an empty `index.html` file and associated JavaScript code to handle things such as routing, logic and AJAX (Asynchronous JavaScript And XML).

#### Advantages
- Very responsive user experience
- Only needs to make one HTTP request to receive the `index.html` file and associated JavaScript code (not including AJAX calls). Typically, the initial load of the page is comparatively slow, however, subsequent navigation and view updates are very quick 

#### Disadvantages
- Not optimized for SEO (Search Engine Optimization), the initial state of the `index.html` is empty therefore it may not contain content for the bot to crawl
- JavaScript bundle could be large, so if the user has a slower internet connection the initial load could be slow

#### Technologies
- [React](https://reactjs.org/) - a very popular front end library developed by Facebook
- [Angular](https://angular.io/) - a popular full-blown framework developed by Google that supports routing, [RxJS](https://rxjs.dev/guide/overview) and [TypeScript](https://www.typescriptlang.org/)
- [Vue.js](https://vuejs.org/) - an emerging library gaining traction with its simplicity

# Server Side Rendering
An alternative to rendering on the browser is to render the view on the server and then send the view to the browser, this is known as SSR. This means the server handles all API/DB calls, rendering logic and generates the view. So when the client receives this response it just needs to display it to the user. SSR is the preferred rendering approach if you are concerned with SEO, as the HTML files will already have content for bots to crawl.

#### Advantages
- SEO friendly
- Ideally, no further AJAX/API calls are required from the client
- Initial load will be quicker than CSR

#### Disadvantages
- If your web application needs to update the view often, SSR may not be the best option because for each update, it will require sending another request to the server
- Response time can be affected if the server is busy

#### Technologies
- [Next.js](https://nextjs.org/) - React
- [Nuxt.js](https://nuxtjs.org/) - Vue.js

# Static Site Generators
Lastly, SSG is similar to SSR in that the server is responsible for rendering the view. The main difference is that files served by SSG are generated at ***build*** time (rather than on request), meaning the views are generating when building the application. So the server's purpose is primarily to serve these files, not generate them. This also highlights the main drawback with this approach, and that is the views served are well, static. So depending on your requirements, SSG may not be a viable option

#### Advantages
- SEO friendly
- Very performant, because the views are already generated and just needs to be served
- Does not require additional AJAX/API calls

#### Disadvantages
- Updates will only be reflected when rebuilding the application
- Static in nature, so mostly applicable to blogs, landing pages etc.

#### Technologies
- [Gatsby](https://www.gatsbyjs.com/) - React
- [Gridsome](https://gridsome.org/) - Vue.js

A hybrid approach is likely to give the most benefits in terms of performance and SEO. By utilizing both CSR **and** SSR, we can achieve both a responsive user experience but also gain the SEO benefits from SSR. The server will render a view with mostly static components (so the initial load is not empty), but also include JavaScript code to handle things such as AJAX and events.