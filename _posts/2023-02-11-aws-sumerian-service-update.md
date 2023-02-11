---
layout: post
title:  "Unavailability of AWS Sumerian Service!"
date:   2023-02-11 00:00:00 +0000
categories: AWS sumerian endoflife service unavailability
---
It was a long term goal to try out AWS's AR/VR 3D Service AWS Sumerian. If you try searching over in the aws console, you will see a service similar to one shared below.

![AWS Sumerian Service search](assets/post_images/2023-02-11/aws-sumerian-service-search.png)

If this is the first time you are accessing AWS Sumerian, clicking on the service, it directs you to the [region-specific home page](https://ap-south-1.console.aws.amazon.com/sumerianv2/home/){:target="_blank"}, then very quickly redirecting you to the [additional-resources page](https://ap-south-1.console.aws.amazon.com/sumerianv2/home/additionalresources#/){:target="_blank"}.

![AWS Sumerian Service Home Page](assets/post_images/2023-02-11/aws-sumerian-home-page.png)

This is very confusing at first, making you think as to did I miss anything and searching google for "AWS Sumerian not loading in chrome", at least in my case :)

Doing some search, I found below info at [the AWS Sumerian Service Page](https://aws.amazon.com/sumerian/){:target="_blank"}.

> The Amazon Sumerian service is no longer accepting new customers. Existing customer scenes will not be available after February 21, 2023. We therefore recommend that you move any existing scenes to the new Babylon.js-AWS experience and publish your web app using a service like AWS Amplify Hosting.

In short, Amazon Sumerian Service is no longer available for use. The service you see in AWS search menu is for existing customers until Feb 21, 2023. I think, it would have been a bit more helpful to see this info in the AWS console page as a hint or notification when AWS sumerian is accessed :)