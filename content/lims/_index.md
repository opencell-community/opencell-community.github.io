---
title: "LIMS"
date: 2022-09-13T12:58:15+01:00
chapter: true
draft: false
---


{{% children description="true" sort="Name" %}}

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


## 📚 Guide



<details>
<summary><b>Routing</b></summary>
<p>
  This project uses <a target="_blank" href="https://reacttraining.com/react-router/web/guides/quick-start">React Router</a> and includes a convenient <code>useRouter</code> hook (located in <code><a href="src/util/router.js">src/util/router.js</a></code>) that wraps React Router and gives all the route methods and data you need.

```js
import { Link, useRouter } from "./../util/router.js";

function MyComponent() {
  // Get the router object
  const router = useRouter();

  // Get value from query string (?postId=123) or route param (/:postId)
  console.log(router.query.postId);

  // Get current pathname
  console.log(router.pathname);

  // Navigate with the <Link> component or with router.push()
  return (
    <div>
      <Link to="/about">About</Link>
      <button onClick={(e) => router.push("/about")}>About</button>
    </div>
  );
}
```
</p>
</details>

<details>
<summary><b>Authentication</b></summary>
<p>
  This project uses <a href="https://firebase.google.com">Firebase Auth</a> and includes a convenient <code>useAuth</code> hook (located in <code><a href="src/util/auth.js">src/util/auth.js</a></code>) that wraps Firebase and gives you common authentication methods. Depending on your needs you may want to edit this file and expose more Firebase functionality.

```js
import { useAuth } from "./../util/auth.js";

function MyComponent() {
  // Get the auth object in any component
  const auth = useAuth();

  // Depending on auth state show signin or signout button
  // auth.user will either be an object, null when loading, or false if signed out
  return (
    <div>
      {auth.user ? (
        <button onClick={(e) => auth.signout()}>Signout</button>
      ) : (
        <button onClick={(e) => auth.signin("hello@divjoy.com", "yolo")}>Signin</button>
      )}
    </div>
  );
}
```
</p>
</details>

<details>
<summary><b>Database</b></summary>
<p>
  This project uses <a href="https://firebase.google.com/products/firestore">Cloud Firestore</a> and includes some data fetching hooks to get you started (located in <code><a href="src/util/db.js">src/util/db.js</a></code>). You'll want to edit that file and add any additional query hooks you need for your project.

```js
import { useAuth } from './../util/auth.js';
import { useItemsByOwner } from './../util/db.js';
import ItemsList from './ItemsList.js';

function ItemsPage(){
  const auth = useAuth();

  // Fetch items by owner
  // Returned status value will be "idle" if we're waiting on
  // the uid value or "loading" if the query is executing.
  const uid = auth.user ? auth.user.uid : undefined;
  const { data: items, status } = useItemsByOwner(uid);

  // Once we have items data render ItemsList component
  return (
    <div>
      {(status === "idle" || status === "loading") ? (
        <span>One moment please</span>
      ) : (
        <ItemsList data={items}>
      )}
    </div>
  );
}
```
</p>
</details>

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
<summary><b>Other</b></summary>
<p>
  This project was created using <a href="https://divjoy.com?ref=readme_other">Divjoy</a>, the React codebase generator. You can find more info in the <a href="https://docs.divjoy.com">Divjoy Docs</a>.
</p>
</details>
  


# Project Configuration


The Opencell BioHotel Lims uses a number of different data sources.

To start the project locally, first install the vercel cli as detailed above.

Data is stored in cloud firestore, create a project and generate a set of credentials which are needed for the following environment variables.

- FIREBASE_PROJECT_ID=
- FIREBASE_AUTH_DOMAIN=
- FIREBASE_API_KEY=
- FIREBASE_PRIVATE_KEY=
- FIREBASE_CLIENT_EMAIL=
- REACT_APP_FIREBASE_PROJECT_ID=
- REACT_APP_FIREBASE_AUTH_DOMAIN=
- REACT_APP_FIREBASE_API_KEY=


This will allow firebase to connect to your app.


The firestore database requires records in some of the following formats:


- Users
  * email
  * role (set as empty or `admin` to enable admin view)
  * workflows (collection created by application)
    + createdAt
    + elements (JSON encoded string of the workflow graph)
    + id (autogenerated)
    + name
  * runs (collection created by application)
    + createdAt
    + id
    + owner (owning user ID)
    + status (string such as `created`)
    + workflow (id of workflow used for the run)

- Cells (collection of cells)
  * blockIdentifier (unique readable name)
  * blockType (`input`, `output`, `default` determines cell join logic)
  * consumables (array)
    + merchandiseGid (shopify item variant id `gid://shopify/Product/6679469129795`)
    + minQuantity
  * cost: (number)
  * createdAt
  * id
  * owner (creating user)
  * primary (primary text)
  * secondary (secondary text)
  * secondaryDesc (description)
  * steptime (time for cell to run, number)
  * instances (collection)
    + labID (id of lab of cell)
    + reference (cell name or identifier)
    + availability (collection, different types `booking` or `closure` allows a continuous period of booking or recurring periods of bookings)
      - if BOOKING TYPE
        * createdAt
        * updatedAt
        * startDate
        * endDate
        * recordType == `booking`
      - IF CLOSURE TYPE
        * createdAt
        * updatedAt
        * startDate
        * endDate
        * recordType == `closure`
        * runningDays : string encoded bitmask of length 7 `01111111`
        * runningHours: string encoded bitmask of length 24 `000001111111000000101110`
        * runID
        * userID
- Labs
  * createdAt
  * id (same as document ID)
  * name (string)
  * owner (creating user document ID)
- Sensors
  * cellInstanceID
  * createdAt
  * id (same as document ID)
  * labID (ID of linked Lab by name)
  * owner (owning user document ID)
  * sensorID: name of Sensor e.g `onewiresensor2` same as registered in IOT core
  * sensorType e.g `tempprobe`


## Graphs

The project uses [CubeJS](https://cube.dev)
 to render sensor data. You can either create an account or host your own instances. the .env file needs an `CUBEJS_API_SECRET=` for graphing and authentication with the service to work

 CubeJs needs to be given access to the BigQuery database in which the sensor data is written.


 ## Data storage and pipelines

 Data for the LIMS is stored in the Firestore instance, sensor data is piped to a BigQuery instance using a standard google cloud dataflow template. (Job name Pub/Sub Topic to BigQuery)


 Data for the sensors is passed from an ESP8266 sensor to the google cloud IOT gateway.


 In addition to this, the data can be analyzed in stream by creating a dataflow pipeline with code from [this repo](https://github.com/UK-CoVid19/incubator-turnoff-model). This model analyzes temperature data and if it breaches a certain threshold will write this error to a message queue.

 Messages from this queue can be consumed by a cloud function and written to an alerts collection in the firestore database.

 n.b use own service account credentials or load from the environment


```js
// * Background Cloud Function to be triggered by Pub/Sub.
// * This function is exported by index.js, and executed when
// * the trigger topic receives a message.
// *
// * @param {object} message The Pub/Sub message.
// * @param {object} context The event metadata.
// */


const { initializeApp, applicationDefault, cert } = require('firebase-admin/app');
const { getFirestore } = require('firebase-admin/firestore');

const serviceAccount = {
    "type": "service_account",
    "project_id": MY_PROJECT_ID,
    "private_key_id": MY_PRIVATE_KEY_ID,
    "private_key": PRIVATE_KEY,
    "client_id": CLIENT_ID,
    "auth_uri": AUTH_URI,
    "token_uri": TOKEN_URI,
    "auth_provider_x509_cert_url": CERT_URL,
    "client_x509_cert_url": X509_CERT_URL
  }
  ;
initializeApp({
    credential: cert(serviceAccount)
});

exports.helloPubSub = async (message, context) => {
    console.log(message, 'message')
    

    const db = getFirestore();
    // get the RUN id and the user ID
    const data = message.data
    let buff = Buffer.from(data, 'base64');  
    let text = buff.toString('utf-8');
    console.log(text)
    const body = JSON.parse(text)
    console.log(body)


    const docRef = db.collection('alerts').doc()

    const resp = await docRef.set(body)
    console.log(resp)
```


## BigQuery Schema

 The following BigQuery schema is a mapping of the data passed from the sensors into the system.

 Typically sensor1 and sensor2 are enabled and used for temperature and humidity data, sensor3 is used for battery voltage.
 
 - timestamp TIMESTAMP REQUIRED
 - deviceId STRING REQUIRED
 - sensor1Id STRING NULLABLE
 - sensor1value NUMERIC NULLABLE
 - sensor2Id STRING NULLABLE
 - sensor2Value NUMERIC NULLABLE
 - sensor3Id STRING NULLABLE
 - sensor3Value NUMERIC NULLABLE


Data is timestamped and linked to a particular sensor, this can be linked to the device / cell / lab as per the firestore schema above.

## Shopify Integration

The LIMS system has a notion of supplies needed to complete runs.

We achieve this by linking the runs and workflow builder to a separate instance of shopify and using it's graphQL api to create baskets of products.

Shopify requires a GraphQL app to be created, a current store and a storefront access token to get data from the store to the client application.

The consumables are to be registed in the companion shopify instance and are to be used as part of the workflow planning stage.

### Shopify function hooks

  As part of the ordering process, the LIMS application needs to know when an order has been placed through shopify. There is a google cloud function provided to update the run with the order ID from shopify using the shopify hooks API.

```js
// * Background Cloud Function to be triggered by Pub/Sub.
// * This function is exported by index.js, and executed when
// * the trigger topic receives a message.
// *
// * @param {object} message The Pub/Sub message.
// * @param {object} context The event metadata.
// */


const { initializeApp, applicationDefault, cert } = require('firebase-admin/app');
const { getFirestore } = require('firebase-admin/firestore');

const serviceAccount = {
    "type": "service_account",
    "project_id": MY_PROJECT_ID,
    "private_key_id": MY_PRIVATE_KEY_ID,
    "private_key": PRIVATE_KEY,
    "client_id": CLIENT_ID,
    "auth_uri": AUTH_URI,
    "token_uri": TOKEN_URI,
    "auth_provider_x509_cert_url": CERT_URL,
    "client_x509_cert_url": X509_CERT_URL
  }
  ;
initializeApp({
    credential: cert(serviceAccount)
});

exports.updateOrder = async (message, context) => {
    console.log(message, 'message')
    

    const db = getFirestore();
    // get the RUN id and the user ID
    const data = message.data
    let buff = Buffer.from(data, 'base64');  
    let text = buff.toString('utf-8');
    console.log(text)
    const body = JSON.parse(text)
    console.log(body)
    const attributes = body.note_attributes
    console.log(attributes) 
    const run = attributes.find(attr => attr.name === "runID")
    if (!run) {
        console.log('not a run order')
        return
    }

    const runID = run.value
    const user = attributes.find(attr => attr.name === "userID")
    if (!user) {
        console.log('invalid as no user id')
        throw new Error("user ID not set")
    }

    const userID = user.value

    const updateData = { runID, userID, orderUrl: body.order_status_url }
    console.log(updateData)

    const docRef = db.collection('users').doc(userID).collection('runs').doc(runID);

    const resp = await docRef.update({ order: updateData, status: 'ordered' })
    console.log(resp)
};



