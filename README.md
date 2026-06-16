# MeshKit Ionic SDK

MeshKit is a TypeScript SDK for decentralized storage on IPFS, built for Ionic applications.

## Quick Example

```ts
import { Meshkit } from "./src/Meshkit";

const mk = await Meshkit.init({
  provider: "pinata",
  providerToken: process.env.PINATA_JWT,
});

const record = await mk.store({ hello: "world" });
const data = await mk.retrieve(record.cid);
console.log(data);
```

## APIs

init · testConnection · store · retrieve · upload · download · send · receive · revoke

See the [docs](./docs/getting-started.md) folder for full documentation.
