---
title: "Deployment"
description: "Deploy the application"
date: 2022-09-14T14:09:20+01:00
draft: false
weight: 8
pre: '<i class="fas fa-cloud-upload-alt"></i> '
---

<details>
<summary><b>Deployment</b></summary>
<p>
Install the Vercel CLI

```
npm install -g vercel
```

Add each variable from your `.env` file to your Vercel project, including the ones prefixed with "REACT_APP\_". You'll be prompted to enter its value and choose one or more environments (development, preview, or production). See <a target="_blank" href="https://vercel.com/docs/environment-variables">Vercel Environment Variables</a> to learn more about how this works, how to update values through the Vercel UI, and how to use secrets for extra security.

```
vercel env add plain VARIABLE_NAME
```

Run this command to deploy to a unique preview URL. Your "preview" environment variables will be used.

```
vercel
```

Run this command to deploy to your production domain. Your "production" environment variables will be used.

```
vercel --prod
```

See <a target="_blank" href="https://vercel.com/docs/platform/deployments">Vercel Deployments</a> for more details.
</p>
</details>

<details>