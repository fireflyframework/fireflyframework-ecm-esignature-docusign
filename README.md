# Firefly ECM eSignature – DocuSign

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21+-orange.svg)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)

DocuSign eSignature adapter for Firefly fireflyframework-ecm. Uses the official DocuSign Java SDK and exposes the fireflyframework-ecm eSignature ports.

## Features
- Envelope lifecycle: create, get, update, send, void, archive (basic mapping)
- JWT OAuth flow via DocuSign SDK (signature + impersonation scopes)
- Optional sandbox mode that switches to demo endpoints
- Spring Boot auto-configuration for `ApiClient` and conditional bean wiring

## Installation
```xml
<dependency>
  <groupId>org.fireflyframework</groupId>
  <artifactId>fireflyframework-ecm-esignature-docusign</artifactId>
  <version>${firefly.version}</version>
</dependency>
```

## Configuration
```yaml
firefly:
  ecm:
    enabled: true
    features:
      esignature: true
    esignature:
      provider: docusign
    adapter:
      docusign:
        integration-key: ${DOCUSIGN_INTEGRATION_KEY}
        user-id: ${DOCUSIGN_USER_ID}
        account-id: ${DOCUSIGN_ACCOUNT_ID}
        private-key: ${DOCUSIGN_PRIVATE_KEY}  # PEM string or loaded via env/secret manager
        # optional
        sandbox-mode: ${DOCUSIGN_SANDBOX:false}
        base-url: https://na3.docusign.net/restapi
        auth-server: https://account.docusign.com
        connection-timeout: 30s
        read-timeout: 60s
        max-retries: 3
        jwt-expiration: 3600
        enable-polling: true
        polling-interval: 5m
        default-email-subject: "Please sign this document"
        default-email-message: "Please review and sign the attached document(s)."
```

Activation
- Auto-config class initializes `ApiClient` and requests a JWT user token; set `sandbox-mode: true` to use demo endpoints.

## Usage
```java
@Autowired SignatureEnvelopePort envelopePort;
SignatureEnvelope draft = SignatureEnvelope.builder()
    .title("MSA")
    .description("Please sign")
    .build();
SignatureEnvelope created = envelopePort.createEnvelope(draft).block();
envelopePort.sendEnvelope(created.getId(), null).block();
```

Notes
- Embedded signing URL is not implemented in this adapter.
- Document/recipient mapping in `buildEnvelopeDefinition` is minimal and intended to be extended.

## Testing
- Includes a Spring Boot smoke test that verifies the adapter bean loads when provider is `docusign`.

## License
Apache 2.0
