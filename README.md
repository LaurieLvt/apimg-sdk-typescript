# APIMG TypeScript and Javascript SDK Library

Typescript and Javascript SDK for the [Apimg](https://apimg.fr/) API

Environment
* Node.js
* Webpack
* Browserify

Language level
* ES5 - you must have a Promises/A+ library installed
* ES6

Module system
* CommonJS
* ES6 module system

It can be used in both TypeScript and JavaScript. In TypeScript, the definition should be automatically resolved via `package.json`. ([Reference](http://www.typescriptlang.org/docs/handbook/typings-for-npm-packages.html))

## Requirements

You need to have an Apimg account in order to use the SDK. To do so, please [take an appointment](https://calendar.app.google/exNdKbAPdYxjcDrM7) with the team to be guided in your configuration, otherwise [register yourself](https://app.apimg.fr/#/signup) directly.

You will have 14 days of free access once registered. If you want to subscribe to a plan, please [take an appointment](https://calendar.app.google/exNdKbAPdYxjcDrM7) with the team.

## Installation

```
npm install apimg-sdk-typescript --save
```

## API Documentation

You will find a Swagger API documentation [here](https://app.apimg.fr/#/api-documentation)

## SDK Usage

### Importing and Initializing the SDK

```typescript
// Importing the DefaultApi class and the configuration
import { DefaultApi, Configuration } from 'apimg-sdk-typescript';

// Configuring the client with your access token
const configuration = new Configuration({
  accessToken: 'your-access-token', // Replace with your access token
  apiKey: 'your-api-key', // Replace with your API KEY retrieved from https://app.apimg.fr/#/dashboard/profile or from "getApiKey" method
  refreshToken: 'your-refresh-token', // Replace with your Refresh Token retrieved from https://app.apimg.fr/#/dashboard/profile or from "getAccessToken" method, which renews both the access token and the refresh token
});

// Initializing the client
const apimgClient = new DefaultApi(configuration);
```

---

### Example: Retrieve Matching Results (`getMatchingResults`)

```typescript
try {
    const requestBody = {
        userId: '12345', // Replace with the user ID stored in your DB
        page: 1, // page number
        limit: 10, // number of results in the page
    };

    const response = await apimgClient.getMatchingResults(requestBody);
    console.log('Matching results:', response.data);
} catch (error) {
    console.error('Error while retrieving matching results:', error);
}
```

**Example Response:**
```json
{
    "page": 1,
    "matching_results": [
        {
            "id": "id_match_1",
            "matching_score": 4535.8121375166265,
            "matching_score_percent": 45.32,
        },
        {
            "id": "id_match_2",
            "matching_score": 3379.9537032329235,
            "matching_score_percent": 33.77,
        }
    ]
}
```

---

#### Example: Obtain an Access Token (`getAccessToken`)

```typescript
try {
    const response = await apimgClient.getAccessToken();
    console.log('Access token:', response.data);
} catch (error) {
    console.error('Error while retrieving the access token:', error);
}
```

**Example Response:**
```json
{
    "accessToken": "eyJhbGc...HjykfCs",
    "accessTokenExpireAt": 1746096065,
    "refreshToken": "eyJhbGc...GcOpFQag",
    "refreshTokenExpireAt": 1753807265
}
```

---

For more details on the available methods, please refer to [the documentation](https://app.apimg.fr/#/api-documentation) or explore the types and methods exposed by the SDK.