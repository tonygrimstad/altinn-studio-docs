---
title: Get Started with Altinn Correspondence as a Service Owner
linktitle: Service Owner
description: How to get started with Altinn 3 Correspondence, for service owners
tags: [Correspondence, guide]
toc: true
weight: 10
---

{{<children />}}

{{% notice warning  %}}
This process will be simplified through a future update in Altinn Studio.

Particularly Steps 4-6 will be performed through GUI instead of requiring direct API Calls.
{{% /notice %}}

## 1. Get started as service owner in Altinn {#get-started-as-service-owner-in-altinn}

To get started with Altinn Correspondence, your enterprise must be registered as a service owner in Altinn. For a step-by-step guide , see the
[Get started with Altinn guide (Norwegian language only)](https://www.altinndigital.no/kom-i-gang/guide-kom-i-gang-med-altinn/).

This step is only necessary for new enterprises that have not yet established themselves as service owners on the Altinn platform. As an existing service owner, you can proceed directly with the next steps to start using Altinn Correspondence.

## 2. Perform common steps for API Key and Maskinporten Client {#perform-common-steps-for-api-key-and-maskinporten-client}

Perform steps 1 and 2 of the [Common Get started steps](../common-steps) if you have not already done so.

## 3. Register a Resource in Altinn Resource Registry {#register-a-resource-in-altinn-resource-registry}
In order to send messages via Altinn Correspondence, they must first be associated with a resource. 
A resource represents a specific function or set of functions used to manage access and rules for the correspondence. 
Resources are registered via Altinn Studio and are used to define access rules and access lists, ensuring that only authorized users can perform specific actions.

Your policy must be configured in such a way that that they permit the actions:
1. Log in to Altinn Studio and navigate to the resource dashboard, See [Resource Registry](../../../../authorization/guides/create-resource-resource-admin/) for a detailed guide.
2. Create a new resource, follow the guide and fill in the necessary information and details about the service.
3. Set policy rules for the resource. Your policy must be configured in such a way that that they permit the actions:
    - "read" meant for recipients to open and read a message
    - "write" meant for senders to send a message
    - "subscribe" to register event subscriptions in Altinn Events

Here is an [example policy](ExamplePolicy.xml).

Note that this example policy sets a required user role "DAGL" for the user that has access to the resource, and requires the use of [Resource Rights Registry](../../../../authorization/what-do-you-get/resourceregistry/rrr/) to grant access to specific organisations.
A user with that access can then delegate the access to the enterprise user / system user

**TIP**: Verify your configurations using the [Postman collection](https://github.com/Altinn/altinn-correspondence/blob/main/altinn-correspondence-postman-collection.json), substituting the test tokens with your own Altinn tokens (See "Login to Maskinporten (Initialize)" request in Authenticator folder).



