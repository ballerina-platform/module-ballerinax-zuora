## Overview

[Zuora](https://www.zuora.com/) is a leading cloud-based subscription management platform that helps businesses manage subscription billing, finance, and revenue recognition. It provides comprehensive tools for subscription management, billing, payments, and revenue automation, enabling businesses to launch and scale subscription-based services efficiently.

The `ballerinax/zuora` package provides a client API to connect to the Zuora REST API using Ballerina.

The Ballerina Zuora connector is compatible with the [`Zuora V1 REST API`](https://developer.zuora.com/rest-api/rest-api-introduction/).

## Setup guide

// TODO: update setup guide

## Quickstart

To use the Zuora connector in your Ballerina application, modify the `.bal` file as follows:

### Step 1: Import the module

Import `ballerinax/zuora` module into your Ballerina project.

```ballerina
import ballerinax/zuora;
```

### Step 2: Instantiate a new connector

Create an `zuora:Client` object with your domain URL and relevant authentication options.

```ballerina
configurable string clientId = ?;
configurable string clientSecret = ?;
configurable string tokenUrl = ?;
configurable string baseUrl = ?;

zuora:ConnectionConfig configuration = {
    auth: {
        clientId, 
        clientSecret, 
        tokenUrl
    }
};

zuora:Client zuora = check new (configuration, baseUrl);
```

### Step 3: Invoke the connector operations

Now, utilize the available connector operations.

#### List all products

```ballerina
zuora:GETCatalogType products = check zuora->/v1/catalog/products(zuoraVersion = "341.0");
```

#### Retrieve a specific product

```ballerina
zuora:GETProductType product = check zuora->/v1/catalog/products/["2c92c0f94a07c086014a13f4af9612e4"](zuoraVersion = "341.0");
```

#### Create a subscription

```ballerina
zuora:POSTSubscriptionType subscription = {
    accountKey: "A00001234",
    contractEffectiveDate: "2023-01-01",
    termType: "TERMED",
    autoRenew: false,
    initialTerm: 12,
    renewalTerm: 12,
    subscribeToRatePlans: [
        { productRatePlanId: "2c92c0f94a07c086014a13f4af9612e4"}
    ]
};
zuora:POSTSubscriptionResponseType createSubscriptionResponse = check zuora->/v1/subscriptions.post(subscription, zuoraVersion = "341.0");
```

### Step 4: Run the Ballerina application

```Shell
bal run
```

## Examples
