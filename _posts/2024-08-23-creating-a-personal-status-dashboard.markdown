---
layout: post
title:  "Building a Personal Dashboard: Automating Life’s Essential Checks – Part 1"
date:    2024-08-23 13:37:00 +1000
categories: nodejs building 
---

#### Introduction

Although I've been programming in Python for years, I've always been curious about other languages and technologies.

For a while now, I've been wanting to dive into `Node.js`, but I hadn't found the right project to push me to start learning. Recently, I listened `o an inspiring episode of Lex Fridman's podcast where [he interviewed Pieter Levels](https://youtu.be/oFtjKbXKqbg?si=HHh5lMkiMqoW0ejd), a digital nomad and developer known for his ability to ship products quickly. Pieter's approach to development—focusing on solving problems fast and iterating later—really resonated with me. I even bought his book [readMake](https://readmake.com/). It made me realize that I don’t need to wait for the perfect idea or project to start coding. I just need to begin.

With this in mind, I decided to combine my interest in Node.js with a practical need: *automating the essential checks I perform daily in my life*.

This marks the beginning of a project to build a personal dashboard where I can monitor various aspects of my life. In this first post of the series, I’ll walk you through the initial step: setting up a simple Node.js app that checks the status of my personal blog.

#### Why Automate Life Checks?

We all have routine checks that we perform regularly—whether it's ensuring our blog is up and running, checking for unread emails, or making sure we've paid our bills on time. These tasks can be tedious and easy to forget. By automating these checks, I can free up mental space and focus on more important things.

For me, this project isn’t just about practicality; it’s also a personal challenge. Inspired by Pieter Levels, I wanted to prove to myself that I can ship something quickly that actually solves a problem, no matter how small. The app may not do much right now, but it’s up and running, and that’s a first step.

#### Part 1: Setting Up a Blog Status Checker

##### Project Setup

To kick off this project, I decided to start with a simple check to monitor the uptime of my personal blog. This was a great way to get my hands dirty with Node.js and TypeScript.

Here’s how I set up the project:

```bash
mkdir status-page-ts
cd status-page-ts
npm init -y
npm install typescript axios
npx tsc --init
```

This initialized a Node.js project with TypeScript and installed `axios` for making HTTP requests.

##### Writing the Blog Status Check

Next, I wrote a simple script to check whether my blog is online. This script sends a request to the blog’s URL and returns whether the blog is up or down:

```typescript
import axios from 'axios';

export async function checkBlogStatus(): Promise<{ status: string; color: string }> {
    try {
        const response = await axios.get('https://adolfovillalobos.github.io/website');
        return {
            status: response.status === 200 ? 'Online' : 'Offline',
            color: response.status === 200 ? 'green' : 'red',
        };
    } catch (error) {
        return {
            status: 'Offline',
            color: 'red',
        };
    }
}
```

This function uses `axios` to send a GET request to my blog. If the response is successful, it returns an "Online" status; otherwise, it returns "Offline".

##### Deploying to Heroku

With the status check script working, I wanted to deploy it so that I could access it from anywhere. Inspired by Pieter’s rapid shipping philosophy, I chose Heroku for its simplicity and free tier.

Here’s how I deployed the app:

1. **Set Up Heroku**: I installed the Heroku CLI, logged in, and created a new Heroku app.
2. **Deploy the App**: I pushed my code to Heroku, configured it to serve the status page, and made sure everything was running smoothly.
3. **Set Up a Custom Domain**: I configured my GoDaddy domain to point to the Heroku app, so I could access the status page at a more personalized URL.

**Troubleshooting**:
I ran into a few issues along the way, like missing the `start` script in `package.json` and port binding errors. These were quickly resolved, and I documented the fixes in case they help anyone else.

I also discovered a GitHub Action in the Heroku documentation that automatically deploys the app when I push to the `main` branch.  

**Note**: In the future, you should consider setting up a CI/CD pipeline to automate the deployment process and run tests and checks before deploying to production. Just sayin!.

##### Viewing the Status Page

With the app deployed, I could now check the status of my blog from anywhere. I set up a simple HTML page that displays the status and color of the blog:

![Blog Status](../assets/images/2024-08-23-final-result-status-page.png)

##### What’s Next?

This is just the beginning. My plan is to expand this dashboard by adding checks for unread emails, monitoring social media inboxes, and even tracking whether I’ve paid my credit cards. The goal is to have a single page that gives me a quick overview of everything important in my life, all in one place.

I know the app is pretty basic right now, but the important thing is that I shipped something. The inspiration I got from Pieter Levels was all about taking action, and I’m excited to continue building on this foundation.



#### Conclusion

In this first post of the series, I shared how I set up a basic Node.js app to monitor the status of my blog and deployed it to Heroku. This project is a step towards automating my daily routine, and I’m excited to see how it evolves.

What would you automate if you had a personal dashboard? Let me know in the comments, and stay tuned for the next part of this series, where I’ll be adding more features to the dashboard!

---
