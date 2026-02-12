# Firefly Framework - ECM eSignature - DocuSign

[![CI](https://github.com/fireflyframework/fireflyframework-ecm-esignature-docusign/actions/workflows/ci.yml/badge.svg)](https://github.com/fireflyframework/fireflyframework-ecm-esignature-docusign/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21%2B-orange.svg)](https://openjdk.org)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)

> DocuSign eSignature adapter for Firefly ECM.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

This module implements the Firefly ECM e-signature ports using DocuSign as the provider. It provides `DocuSignSignatureEnvelopeAdapter` which integrates with DocuSign's eSignature REST API for envelope creation, recipient management, and signing ceremony orchestration.

The adapter auto-configures via `DocuSignAdapterAutoConfiguration` and is activated by including this module on the classpath alongside the ECM core module.

## Features

- DocuSign integration for e-signature envelope management
- Spring Boot auto-configuration for seamless activation
- Implements Firefly ECM SignatureEnvelopePort
- Configurable via application properties
- Standalone provider library (include alongside fireflyframework-ecm)

## Requirements

- Java 21+
- Spring Boot 3.x
- Maven 3.9+
- DocuSign account and API credentials

## Installation

```xml
<dependency>
    <groupId>org.fireflyframework</groupId>
    <artifactId>fireflyframework-ecm-esignature-docusign</artifactId>
    <version>26.02.02</version>
</dependency>
```

## Quick Start

The adapter is automatically activated when included on the classpath with the ECM core module:

```xml
<dependencies>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-ecm</artifactId>
    </dependency>
    <dependency>
        <groupId>org.fireflyframework</groupId>
        <artifactId>fireflyframework-ecm-esignature-docusign</artifactId>
    </dependency>
</dependencies>
```

## Configuration

```yaml
firefly:
  ecm:
    esignature:
      docusign:
        base-url: https://demo.docusign.net
        account-id: your-account-id
        integration-key: your-integration-key
```

## Documentation

No additional documentation available for this project.

## Contributing

Contributions are welcome. Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details on our code of conduct, development process, and how to submit pull requests.

## License

Copyright 2024-2026 Firefly Software Solutions Inc.

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
