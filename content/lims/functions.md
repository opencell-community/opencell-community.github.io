---
title: "Functions"
date: 2022-09-14T16:45:22+01:00
description: "Hook functions for processing orders and other backend tasks"
draft: false
---

##

The LIMS system has some backend functionality to process events.

When a user places an order using the shopify integration, a handler function receives the order complete message and update the database with the completed order identifier.

Subscribe to the `orders/create` or `orders/paid` events for this hook.

https://shopify.dev/api/admin-rest/2022-10/resources/webhook



``` javascript

/ * Background Cloud Function to be triggered by Pub/Sub.
// * This function is exported by index.js, and executed when
// * the trigger topic receives a message.
// *
// * @param {object} message The Pub/Sub message.
// * @param {object} context The event metadata.
// */


const { initializeApp, applicationDefault, cert } = require('firebase-admin/app');
const { getFirestore } = require('firebase-admin/firestore');

const serviceAccount = GCLOUD SERVICE ACCOUNT OBJECT;


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
    const body = JSON.parse(text)
    const attributes = body.note_attributes
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

    const docRef = db.collection('users').doc(userID).collection('runs').doc(runID);

    const resp = await docRef.update({ order: updateData, status: 'ordered' })   
};

```