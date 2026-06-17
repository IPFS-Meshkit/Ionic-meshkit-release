# MeshKit Ionic SDK

MeshKit is a developer-friendly TypeScript SDK that brings decentralized storage capabilities to Ionic applications using IPFS.

It provides a simple API for storing JSON data, uploading files, retrieving content, sending messages, and managing IPFS-backed application data without requiring developers to understand the underlying IPFS infrastructure.

---

## Features

* IPFS-powered decentralized storage
* Simple Ionic-friendly TypeScript API
* JSON storage and retrieval
* File upload and download
* Messaging APIs
* Content revocation (unpinning)
* Pinata provider integration
* Strong TypeScript typings
* Comprehensive API documentation
* Automated test suite

---

## Installation

```bash
npm install @meshkit/ionic
```

---

## Quick Start

```ts
import { Meshkit } from "@meshkit/ionic";

const mk = await Meshkit.init({
  provider: "pinata",
  providerToken: "PINATA_JWT",
});

// Store JSON
const record = await mk.store({
  hello: "world",
});

// Retrieve JSON
const data = await mk.retrieve(record.cid);

console.log(data);
```

---

## Supported Providers

| Provider | Status       |
| -------- | ------------ |
| Pinata   | ✅ Supported  |
| Filebase | 🚧 Planned   |
| Storacha | ❌ Deprecated |

---

## API Overview

### Initialization

```ts
const mk = await Meshkit.init({
  provider: "pinata",
  providerToken: "PINATA_JWT",
});
```

### Connectivity

```ts
await mk.testConnection();
```

### JSON Storage

```ts
const record = await mk.store({
  name: "Alice",
  role: "Developer",
});

const data = await mk.retrieve(record.cid);
```

### File Storage

```ts
const uploaded = await mk.upload(file);

const downloaded = await mk.download(uploaded.cid);
```

### Messaging

```ts
const message = await mk.send(
  "user_123",
  "Hello from MeshKit"
);

const received = await mk.receive(message.cid);
```

### Revocation

```ts
await mk.revoke(cid);
```

---

## Available APIs

| API                | Description                   |
| ------------------ | ----------------------------- |
| `init()`           | Initialize MeshKit            |
| `testConnection()` | Validate provider credentials |
| `store()`          | Store JSON data               |
| `retrieve()`       | Retrieve JSON data            |
| `upload()`         | Upload files                  |
| `download()`       | Download files                |
| `send()`           | Send messages                 |
| `receive()`        | Receive messages              |
| `revoke()`         | Unpin and revoke content      |

---

## Testing

MeshKit includes a comprehensive automated test suite.

### Current Coverage

* 8 Test Files
* 40 Passing Tests

Run tests locally:

```bash
npm test
```

Run coverage:

```bash
npm run test:coverage
```

---

## Build

Compile the SDK:

```bash
npm run build
```

Generated artifacts are emitted to:

```text
dist/
├── Meshkit.js
├── Meshkit.d.ts
├── types.js
├── types.d.ts
├── errors.js
├── errors.d.ts
└── providers/
```

---

## Documentation

Complete documentation is available in the `docs/` directory.

### Getting Started

* docs/getting-started.md
* docs/installation.md
* docs/authentication.md

### Core Documentation

* docs/architecture.md
* docs/error-handling.md
* docs/api-reference.md

### API Reference

* docs/api/init.md
* docs/api/testConnection.md
* docs/api/store.md
* docs/api/retrieve.md
* docs/api/upload.md
* docs/api/download.md
* docs/api/send.md
* docs/api/receive.md
* docs/api/revoke.md

---

## Architecture

```text
Application
      │
      ▼
   MeshKit
      │
      ▼
 Storage Provider
      │
      ▼
    Pinata
      │
      ▼
      IPFS
```

MeshKit abstracts provider-specific implementation details and exposes a consistent developer experience across supported storage providers.

---

## Roadmap

* Filebase Provider
* Encryption Layer Integration
* React Native SDK
* Flutter SDK
* Multi-provider Failover
* CI/CD Release Pipeline
* Package Publishing

---

## License

MIT License
