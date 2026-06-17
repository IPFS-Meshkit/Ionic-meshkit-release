# MeshKit Ionic SDK

> A developer-friendly TypeScript SDK for adding IPFS-backed decentralized storage, file handling, and messaging workflows to Ionic applications.

MeshKit gives Ionic developers a clean SDK layer over decentralized storage providers. It lets applications store JSON, upload and download files, exchange IPFS-backed messages, retrieve content, and revoke pinned data without forcing application teams to manage provider-specific IPFS implementation details.

## Badges

[![npm version](https://img.shields.io/badge/npm-coming%20soon-lightgrey)](#)
[![build](https://img.shields.io/badge/build-passing-brightgreen)](#)
[![tests](https://img.shields.io/badge/tests-40%20passing-brightgreen)](#)
[![license](https://img.shields.io/badge/license-MIT-blue)](#license)
[![typescript](https://img.shields.io/badge/TypeScript-ready-blue)](#)

## Table of Contents

- [Why MeshKit?](#why-meshkit)
- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [API Overview](#api-overview)
- [Supported Providers](#supported-providers)
- [Architecture](#architecture)
- [Testing & Validation](#testing--validation)
- [Documentation & Resources](#documentation--resources)
- [Build](#build)
- [Project Status](#project-status)
- [Roadmap](#roadmap)
- [License](#license)

## Why MeshKit?

IPFS and decentralized storage are powerful, but production apps still need a predictable developer experience. MeshKit wraps provider authentication, content storage, retrieval, file operations, messaging, and revocation behind a small TypeScript API designed for Ionic projects.

Use MeshKit when you want to:

- Add decentralized storage to an Ionic app without building provider integrations from scratch.
- Store structured application data as IPFS-backed JSON records.
- Upload and retrieve files through a consistent SDK interface.
- Validate provider connectivity before running app workflows.
- Keep your app code portable as additional providers are introduced.

## Features

- IPFS-powered decentralized storage for Ionic applications.
- Simple TypeScript SDK with strongly typed APIs.
- JSON storage and retrieval through `store()` and `retrieve()`.
- File upload and download support through `upload()` and `download()`.
- Messaging primitives through `send()` and `receive()`.
- Content revocation through provider-backed unpinning with `revoke()`.
- Pinata provider integration.
- Consistent provider abstraction for future storage backends.
- Automated test coverage for core SDK behavior.
- Public documentation and API validation resources.

## Installation

Install the SDK with your package manager of choice:

```bash
npm install @meshkit/ionic
```

```bash
yarn add @meshkit/ionic
```

```bash
pnpm add @meshkit/ionic
```

You will also need provider credentials. For Pinata, create a JWT token from your Pinata account and pass it to `Meshkit.init()`.

## Quick Start

```ts
import { Meshkit } from "@meshkit/ionic";

const meshkit = await Meshkit.init({
  provider: "pinata",
  providerToken: "PINATA_JWT",
});

await meshkit.testConnection();

const stored = await meshkit.store({
  title: "Hello MeshKit",
  type: "example",
  createdAt: new Date().toISOString(),
});

const data = await meshkit.retrieve(stored.cid);

console.log("Stored CID:", stored.cid);
console.log("Retrieved data:", data);
```

## API Overview

### Initialize

Create a MeshKit client with a supported provider and provider token.

```ts
const meshkit = await Meshkit.init({
  provider: "pinata",
  providerToken: "PINATA_JWT",
});
```

### Test Provider Connectivity

Validate credentials and provider availability before running storage workflows.

```ts
await meshkit.testConnection();
```

### Store and Retrieve JSON

```ts
const record = await meshkit.store({
  name: "Alice",
  role: "Developer",
  project: "MeshKit",
});

const restored = await meshkit.retrieve(record.cid);
```

### Upload and Download Files

```ts
const uploaded = await meshkit.upload(file);

const downloaded = await meshkit.download(uploaded.cid);
```

### Send and Receive Messages

```ts
const message = await meshkit.send("user_123", "Hello from MeshKit");

const received = await meshkit.receive(message.cid);
```

### Revoke Content

```ts
await meshkit.revoke(cid);
```

### Available APIs

| API                | Description                                      |
| ------------------ | ------------------------------------------------ |
| `init()`           | Initialize the SDK with provider configuration.  |
| `testConnection()` | Validate provider credentials and connectivity.  |
| `store()`          | Store JSON data and return a content reference.  |
| `retrieve()`       | Retrieve JSON data by CID.                       |
| `upload()`         | Upload a file to the configured provider.        |
| `download()`       | Download file content by CID.                    |
| `send()`           | Send an IPFS-backed message payload.             |
| `receive()`        | Receive an IPFS-backed message payload.          |
| `revoke()`         | Unpin or revoke provider-backed content by CID.  |

## Supported Providers

| Provider | Status      | Notes                                  |
| -------- | ----------- | -------------------------------------- |
| Pinata   | Supported   | Primary provider integration.          |
| Filebase | Planned     | Targeted for future provider support.  |
| Storacha | Deprecated  | Not planned for active SDK support.    |

## Architecture

MeshKit exposes a stable SDK interface while isolating provider-specific behavior behind storage provider adapters.

```text
Ionic Application
        |
        v
MeshKit TypeScript SDK
        |
        v
Provider Adapter
        |
        v
Pinata / Future Providers
        |
        v
IPFS
```

This structure keeps application code focused on product workflows while MeshKit handles provider configuration, request formatting, content addressing, and API-level consistency.

## Testing & Validation

MeshKit has been validated through automated and manual API testing.

- Postman API validation completed.
- End-to-end testing completed.
- All APIs tested successfully.
- HTTP 200 responses verified for successful API flows.
- Automated test suite includes 8 test files and 40 passing tests.

Run tests locally:

```bash
npm test
```

Run coverage:

```bash
npm run test:coverage
```

## Documentation & Resources

### Live Documentation

- GitBook Documentation:
 [https://bittu-1.gitbook.io/meshkit-documentation](https://bittu-1.gitbook.io/meshkit-documentation)

### API Validation Demo

 [https://drive.google.com/file/d/1HwVDVJuyNuNG_m0kWMDnTwQTYnOoby6Q/view?usp=drivesdk](https://drive.google.com/file/d/1HwVDVJuyNuNG_m0kWMDnTwQTYnOoby6Q/view?usp=drivesdk)

Local documentation is also available in the `docs/` directory:

- `docs/getting-started.md`
- `docs/installation.md`
- `docs/authentication.md`
- `docs/architecture.md`
- `docs/error-handling.md`
- `docs/api-reference.md`
- `docs/api/init.md`
- `docs/api/testConnection.md`
- `docs/api/store.md`
- `docs/api/retrieve.md`
- `docs/api/upload.md`
- `docs/api/download.md`
- `docs/api/send.md`
- `docs/api/receive.md`
- `docs/api/revoke.md`

## Build

Compile the SDK:

```bash
npm run build
```

Generated artifacts are emitted to `dist/`:

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

## Project Status

MeshKit is in active SDK development with a working Pinata provider integration, completed API validation, and passing automated tests. The current focus is stabilizing the public API, improving documentation, and preparing the package for broader public usage.

## Roadmap

- Filebase provider support.
- Encryption layer integration.
- Multi-provider failover.
- React Native SDK exploration.
- Flutter SDK exploration.
- CI/CD release pipeline.
- Public package publishing.

## License

MIT License
