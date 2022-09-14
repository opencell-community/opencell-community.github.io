---
title: "Build"
date: 2022-09-14T14:09:08+01:00
draft: false
---

## 👉 Get Started
Install dependencies
```
npm install
```
Update your `.env` file with values for each environment variable
```
API_KEY=AIzaSyBkkFF0XhNZeWuDmOfEhsgdfX1VBG7WTas
etc ...
```

Install the Vercel CLI
```
npm install -g vercel
```
Link codebase to a Vercel project and run development server
```
vercel dev
```
When the above command completes you'll be able to view your website at `http://localhost:3000`.

_Note: You can run just the front-end with `npm run start`, but `vercel dev` also handles running your API endpoints (located in the `/api` directory)._

## 🥞 Stack
This project uses the following libraries and services:
- Framework - [Create React App](https://create-react-app.dev) with React Router
- UI Kit - [Material UI](https://material-ui.com)
- Authentication - [Firebase Auth](https://firebase.google.com/products/auth)
- Database - [Cloud Firestore](https://firebase.google.com/products/firestore)
- Payments - [Stripe](https://stripe.com)
- Newsletter - [Mailchimp](https://mailchimp.com)
- Contact Form - [Amazon SES](https://aws.amazon.com/ses/)
- Analytics - [Google Analytics](https://googleanalytics.com)
- Hosting - [Vercel](https://vercel.com)