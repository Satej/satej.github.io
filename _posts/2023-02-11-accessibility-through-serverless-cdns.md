---
layout: post
title:  "Accessibility through Serverless CDNs"
date:   2023-02-11 00:00:00 +0000
categories: deno deploy edge deployment cdn serverless
---
Today, we will discussing the evolution of web app deployments focusing on accessibility in particular.

- It started first with a monolithic app bundled together and hosted on a server which in a way resembles below flow. This app typically is deployed on a virtual machine in a particular data center. Challenge with this pattern is it's usually hosted in a single datacenter in a single region. In some cases in multiple regions through a geo-routed load balancer. The cost greatly increases for an ever-on virtual instance even if it is only used for an hour in a day.

![Monolithic Deployment](assets/post_images/2023-02-11/monolithic-deployment.png)

- The second pattern involves two servers. One to host the frontend code built using a SPA framework and the other to host the APIs. The deployment flow looks similar to below. This though helps with the separation of concerns but still has similar side-effects as point 1.

![Frontend Backend Servers Deployment](assets/post_images/2023-02-11/frontend-backend-servers-deployment.png)

- The third pattern involves one server and the frontend being deployed using CDNs which provide the benefits of cached requests at various locations throughout the world at cheaper cost and fast request access to users. The deployment flow looks similar to below. The frontend hosting is self-managed and faster.

![Frontend CDN Deployment](assets/post_images/2023-02-11/frontend-cdn-deployment.png)

- Serverless is the new mode of API deployment taking the pain out of server management. The fourth pattern kind of evolves from the third one above by replacing the hosted server with a CDN hosted serverless deployment of APIs. This now also enables the API requests to be faster by having them closer to the user's location. One such deployment mode is supported by [Deno Deploy](https://deno.com/deploy){:target="_blank"}. You can try it by [signing up](https://deno.com/deploy/pricing){:target="_blank"} for free.

![Frontend Backend CDN Deployment](assets/post_images/2023-02-11/frontend-backend-cdn.png)
