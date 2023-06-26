---
title: "Oryx: Feature sets"
description: Feature sets are collections of standard features
last_updated: May 24, 2023
template: concept-topic-template
---

A *feature set* is a group of related features that can be added to an Oryx application with a single reference. Feature sets simplify the process of setting up an application by reducing the amount of [boilerplate code](/docs/scos/dev/front-end-development/{{page.version}}/oryx/oryx-boilerplate.html) required to configure and initialize the application.

There are two types of feature sets: domain and application feature sets.

## Domain feature sets

A *domain feature set* is an aggregation of the features related to a certain functionality or domain. For example, the product feature set exposes all available product features. This includes components and the associated business logic.

## Application feature sets

An *application feature set* is an aggregation of the features related to a certain business model, such as B2C, B2B, marketplace, or fulfillment. Such feature sets are usually bigger and can include features from different domain feature sets.

Application feature sets can be seen as _demo apps_, because one such set lets you quickly set up a project without developing. However, a standard feature set might be too opinionated for your production application, which is why you might want to extend an existing set or create your own. For more details about creating feature sets, see [Create feature sets](#create-feature-sets).

### Available application feature sets

Oryx includes predefined feature sets that cover common use cases for web applications. The application feature sets are provided in the [presets package](/docs/scos/dev/front-end-development/{{page.version}}/oryx/oryx-presets.html). The following feature sets are available:

- b2cFeatures: features commonly used in B2C applications.
- fulfillmentFeatures: features used in PWAs, used for picking products for fulfillment.

## Labs

The labs package provides experimental features that are not designed for production environments. Experimental features may evolve into standard feature sets over time, but this is not guaranteed. You can use a labs feature set in your demos, POCs, or local development.

## Create feature sets

In addition to the provided feature sets, you can create custom sets tailored to your business requirements. To create a custom set, create an array of feature objects that implement the `AppFeature` interface and pass it to the `withFeature()` method of the `appBuilder()` object. For example:

```ts
import { appBuilder } from "@spryker-oryx/core";
import { customFeature1, customFeature2 } from "/docs/scos/dev/front-end-development/{{page.version}}/oryx/my-features";

const customFeatures = [customFeature1, customFeature2];

const app = appBuilder().withFeature(customFeatures).create();
```
