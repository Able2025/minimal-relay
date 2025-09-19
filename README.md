# Minimal Relay: Decentralized Asset Transfer Protocol

A flexible, secure protocol for managing digital asset transfers, licensing, and rights management on the Stacks blockchain.

## Overview

Minimal Relay provides a robust framework for:
- Decentralized asset ownership tracking
- Flexible licensing and usage rights
- Secure transfer mechanisms
- Creator-centric revenue models

Key Features:
- Multi-tier licensing system
- Transparent transfer and royalty mechanisms
- Programmable usage rights
- Extensible asset management

## Architecture

The protocol consists of two core smart contracts:

```mermaid
graph TD
    A[Relay Core Contract] --> B[Asset Creation]
    A --> C[Ownership Management]
    A --> D[Transfer System]
    A --> E[Revenue Distribution]
    
    F[Licensing Contract] --> G[Usage Rights Configuration]
    F --> H[License Issuance]
    F --> I[Permission Verification]
    F --> J[License Management]
    
    B --> K[Creator Economy]
    C --> K
    D --> K
    E --> K
    G --> L[Flexible Utilization]
    H --> L
    I --> L
    J --> L
```

## Contract Documentation

### Relay Core (`relay-core.clar`)

Manages fundamental asset management functionality:
- Asset creation and ownership tracking
- Transfer mechanics
- Royalty distribution
- Metadata management

### Relay Licensing (`relay-licensing.clar`)

Handles usage rights and licensing:
- Configurable usage tiers
- Dynamic pricing models
- Comprehensive license verification
- Permission tracking

## Getting Started

### Prerequisites
- Clarinet
- Stacks wallet
- STX tokens for transactions

### Basic Usage

1. Creating an asset:
```clarity
(contract-call? .relay-core create-asset "metadata-uri" u100)
```

2. Listing an asset for sale:
```clarity
(contract-call? .relay-core list-asset asset-id price)
```

3. Configuring a license:
```clarity
(contract-call? .relay-licensing configure-license-tier asset-id token-id tier price duration-days max-licenses)
```

## Function Reference

### Core Contract Functions

#### Story Management
```clarity
(create-story (metadata-uri (string-utf8 256)) (royalty-percentage uint))
(update-story-metadata (story-id uint) (new-metadata-uri (string-utf8 256)))
(freeze-story-metadata (story-id uint))
```

#### Trading
```clarity
(list-story (story-id uint) (price uint))
(buy-story (story-id uint))
(make-offer (story-id uint) (offer-price uint) (expiry uint))
(accept-offer (story-id uint) (offerer principal))
```

### Licensing Functions

#### License Management
```clarity
(configure-license-tier (story-id uint) (token-id uint) (tier uint) (price uint) (duration-days uint) (max-licenses (optional uint)))
(purchase-license (story-id uint) (token-id uint) (tier uint))
(renew-license (story-id uint) (token-id uint) (tier uint))
(revoke-license (story-id uint) (token-id uint) (tier uint) (licensee principal))
```

## Development

### Testing
Run tests using Clarinet:
```bash
clarinet test
```

### Local Development
1. Start local chain:
```bash
clarinet integrate
```

2. Deploy contracts:
```bash
clarinet deploy
```

## Security Considerations

### Core Contract
- Royalty calculations use basis points to avoid floating-point issues
- Ownership checks prevent unauthorized transfers
- Metadata freezing prevents post-sale modifications

### Licensing Contract
- License validation prevents unauthorized usage
- Expiration tracking ensures proper access control
- Creator-only license configuration and revocation
- Maximum license count enforcement

### General
- All financial transactions verify sufficient funds
- Access control checks on privileged operations
- State changes are atomic and consistent