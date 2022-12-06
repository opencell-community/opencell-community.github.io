---
title: "Shopify"
date: 2022-09-14T16:41:37+01:00
description: "Link the LIMS runs with the stock orders"
draft: false
pre: '<i class="fas fa-shopping-cart"></i> '
---

## Shopify 

The LIMS system uses an integration with shopify to handle inventory and orders of consumables. 

You need a shopify instance with the GraphQL app client installed.

Generate a `storefrontAccessToken` and use the graphQL API with the `X-Shopify-Storefront-Access-Token` header set.

The URL is of the form:

`https://MY_STORE.myshopify.com/api/2022-01/graphql.json`


Each workflow has consumables that can be purchased, these are linked to the Shopify products by using the product variant GID.

These are stored in the consumables section of a workflow.

The checkout uses the shopify default checkout flow.
