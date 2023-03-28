---
description: Package for Node.js and the browser to integrate Cartesius into your app
---

# JavaScript/TypeScript

With the Cartesius Software-Development-Kit, you can quickly implement the Cartesius API into your web and backend application. To start, install the `@cartesius/sdk` node package.

```bash
  yarn add @cartesius/sdk # or
  npm i @cartesius/sdk
```

You can safely use this package in the browser or with Node.js. Bun and Deno should work as well, but are currently not supported. You can use the package in CommonJS and ESM environments.

```typescript
import { CartesiusClient } from "@cartesius/sdk" // ESM or
const { CartesiusClient } = require("@cartesius/sdk") // CJS

const client = new CartesiusClient({
  apiKey: '<YOUR-API-KEY>',
});

const result = await client.autocomplete("Freiheitsst", {
  languages: ["deu", "en"], // ISO 3166 ALPHA-2 or ALPHA-3
  fields: ["shape", "displayValue", "category"],
  // ...
})
```

As a result, you will receive `CartesiusApiResponse<CartesiusGeoFeature[]>` which is equivalent to the API response you would receive over HTTP.&#x20;

Each method is named after the REST endpoint of the API. The naming of the query parameters is also identical.

The package is **non-throwing**, every error will be represented as `CartesiusApiResponse`, which is equivalent to the API response you would receive over HTTP. Success is being indicated with the `status` property and the HTTP Status code `code`. If there has been an error with the request on the client side, the response will have the code -1. Check the messages for a detailed error descriptions.

###

\
